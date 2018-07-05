---
layout: post
title:      "Rails App with a jQuery Front End "
date:       2018-07-05 10:49:45 +0000
permalink:  rails_app_with_a_jquery_front_end
---


In my latest project I upgraded my Opportunity-Finder Application by adding a jQuery front end to make my application run smoother, and allow Opportunity Providers the convience of seeing information on who applied to their opportunities without refreshing the page, and allowing them to post opportunities without having to do a page refresh. It made the website run a lot smoother. 

## Hijacking

In order to stop the application from changing to a different view, and loading a new page, I had to Hijack the actions being taken by the website by default by using   e.preventDefault(); in my .js file

Doing so, I allowed the application to send out it's requests to the server, but preventing the page from loading a seperate page. 

## Creating  an Opportunity with  AJAX


After Hijacking my post request for a new opportunity, I had to serialize the data so I can append the values to my template. 

```
    var $form = $(this);
    var action = $form.attr("action");
    var params = $form.serialize();
```

$form represents the form that I just submitted.
The variable action is the action of what the request will take, which is "/opportunities". 
params serializes the form that I submitted which is the parameters of the Title and Description that I just submitted.

### The AJAX request

After I serialized the data, I needed to make an AJAX request. 

```
       $.ajax({
      url: action,
      data: params,
      dataType: "json",
      method: "POST"
    })
```
		
You can see that I am now using the previously defined variables.  The url is the action that I am making "/opportunities." The data it needs is the parameters I just sent. I am also wanting the data type to be in JavaScript Object Notation(JSON). 
		
		
### Success!

After the AJAX request is completed, I now want to append this data to the DOM. 


```
.success(function(json){
      var opportunity = new Opportunity(json);
      var opportunityDiv = opportunity.renderDiv()
      $("div.new_opportunity").append(opportunityDiv)
    })
  });
})
```

This function translates my JSON response into a JavaScript Model Object, and uses the function to render the div that is appended onto my page.

```

function Opportunity(attributes){
  this.title = attributes.title;
  this.id = attributes.id;
  this.description = attributes.description;
}

$(function () {
  Opportunity.templateSource = $("#applicant").html();
  Opportunity.template = Handlebars.compile(Opportunity.templateSource);
})

Opportunity.prototype.renderDiv = function() {
  return Opportunity.template(this)
};
```

After translating my JSON response, I use a template to input the data. I used Handlebars, because it is a great template engine that makes it easier to code and read, rather than concatenating all the HTML I want appended onto the page. 

### Handlebars!


```
<script id="applicant" type="text/x-handlebars-template">
    <div id="body-{{id}}">
      <h2>Opportunity Title:  {{title}} </h2>
      <h2>Opportunity Description: {{description}} </h2>
    </div>
  </script>
</body>
```

Using a handlebars template, I was able to have all of my HTML, and input the parameters by their names from the JavaScript Model Object, using the double curly brackets {{example}}. 

This made it a lot easier as I did not have to create ugly and frustrating concatenation. 


## Completed!

I have learned a lot from completing this project, and now knowing how to use JQUERY, I feel that I am able to create a smoother feeling website that keeps the visitors of my site pleased, and not having to wait for a page refresh to view the results. 

![I want my data now](https://media.giphy.com/media/k0BRESevW4VFe/giphy.gif)

Thank you for reading, and you can check out my Opportunity-Finder app [here](https://github.com/gringobrasiliero/opportunity-finder)






