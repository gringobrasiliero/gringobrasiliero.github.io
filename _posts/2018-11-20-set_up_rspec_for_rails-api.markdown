---
layout: post
title:      "Set up Rspec for Rails-api"
date:       2018-11-20 10:57:01 +0000
permalink:  set_up_rspec_for_rails-api
---


Getting started with rspec testing for your Api.

RSpec is a DSL that is used to test your ruby code. It is essential to use when you are testing your back end, and you need to write tests to make sure all of your code is working. When you are creating a ruby backend, you need to write your own tests. This week, I will be going over how to set up rspec for your Rails API.
You can start your new project by calling “rails new project_name –api -T”. using the –api will configure your rails application to be used as an api. The -T tag will exclude Minitest, which is the default testing framework. 

After the rails app gets created, lets fix up the gem file.

```
group :test do
  gem 'factory_bot_rails', '~> 4.0'
  gem 'shoulda-matchers', '~> 3.1'
  gem 'faker'
  gem 'database_cleaner'
end

group :development, :test do
  gem 'rspec-rails', '~> 3.5'
end
```
The Faker gem helps generate fake data, such as names, addresses, and phone numbers. Factory-bot helps us create objects with a predefined set of values. Shoulda-matchers is gem that provides rspec with one-liners that test common Rails functionality. Database-cleaner helps to clean out the database, and delete the created objects after the testing is run. 
After you add these gems into the gem file, run bundle install. 

We then have to run “rails g rspec:install”. This will install rspec and also create the spec directory. 
Lets then get into spec/rails_helper.rb and add the following code to set up our database cleaner, as well as set up our Shoulda-matchers.

```
# require database cleaner at the top level
require 'database_cleaner'

# [...]
# configure shoulda matchers to use rspec as the test framework and full matcher libraries for rails
Shoulda::Matchers.configure do |config|
  config.integrate do |with|
    with.test_framework :rspec
    with.library :rails
  end
end

# [...]
RSpec.configure do |config|
  # [...]
  # add `FactoryBot` methods
  config.include FactoryBot::Syntax::Methods

  # start by truncating all the tables but then use the faster transaction strategy the rest of the time.
  config.before(:suite) do
    DatabaseCleaner.clean_with(:truncation)
    DatabaseCleaner.strategy = :transaction
  end

  # start the transaction strategy as examples are run
  config.around(:each) do |example|
    DatabaseCleaner.cleaning do
      example.run
    end
  end
  /# [...]
end
```

Now, we can make rspec tests for our api. When we write tests for our requests to our api, we need to set up the rspec tests as a “type: :request”.
```
require 'rails_helper'

RSpec.describe 'Todos API', type: :request do
  # initialize test data 
  let!(:todos) { create_list(:todo, 10) }
  let(:todo_id) { todos.first.id }

  # Test suite for GET /todos
  describe 'GET /todos' do
    # make HTTP get request before each example
    before { get '/todos' }
    it 'returns todos' do
      # Note `json` is a custom helper to parse JSON responses
      expect(json).not_to be_empty
      expect(json.size).to eq(10)
    end
```
Note that when we described the Rspec test, we gave it a “type: request”. We then created a list of todos, and made the todo_id equal to the first id, which would be 1. We then write our tests like we normally would. We describe what the test is, then do our before action, as well as what we expect to happen after. 
We need to write a helper method for our JSON, so make a directory inside of your spec folder called support, and create a file called “request_spec_helper.rb”, and put in the following code. 

```
# spec/support/request_spec_helper
module RequestSpecHelper
  # Parse JSON response to ruby hash
  def json
    JSON.parse(response.body)
  end
end
```

We then need to add this support directory into our rails_helper.

```
RSpec.configuration do |config|
  # [...]
  config.include RequestSpecHelper, type: :request
  # [...]
end
```

We then can run the command rspec, and it will then run our first test. 
This is how we get started on writing tests for our rails-api. Being familiar with how to write tests will help your development process, and make it run a lot smoother. Thanks for reading, and I hope you have a wonderful Thanksgiving!


