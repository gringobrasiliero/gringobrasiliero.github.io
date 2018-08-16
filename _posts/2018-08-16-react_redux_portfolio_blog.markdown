---
layout: post
title:      "React Redux Portfolio Blog"
date:       2018-08-16 11:25:21 +0000
permalink:  react_redux_portfolio_blog
---



I decided to do my React-Redux project on an application called Neddit. With so many news articles being posted daily, I wanted to have a place where people could save relevant and “Neddit-worthy” articles to read. When you click on the “Neddit Button, it automatically saves the article associated to the category it belongs to, so visitors can search through new articles, or visit the Post page, and view the articles that others have already deemed Neddit worthy. Visitors can also view the show page for each article that has been saved and leave a comment! 
I used news-api to pull news articles and created my own API to save the new categories, posts, and comments into the database. Doing so, I was able to grab the newest articles from the news-api in JSON format and use that data to place all of the articles onto my page.

Since not all articles are worth storing, I only used GET requests to render the data, and when you Neddit an article, it grabs all that data, and does a POST request to the Posts table. Saving only the articles that are liked allows my database to not be flooded with useless information.


I used my Article component to listen for the Neddit worthy articles, and when you click on the Neddit button, it creates an action, which in this case, does a POST fetch request to Posts. Doing the fetch request, it returns a promise, which is an object that represents a value that will be available later. We have access to the data when the promise is resolved. Chaining then() functions, we are able to access the data that our methods are promising to return. This is an important to do, as without using asynchronous actions with middleware, that data will not be ready to use by the time the compiler goes to the next line. 


Middleware such as Thunk is like the food dresser at a restaurant. Food runners are waiting “patiently” to grab food for their customers, and the food dresser is telling them “Wait! The data is almost ready to be delivered!” Without the food dresser, there would be a lot of unhappy customers, and without the Middleware, we would get a lot of Compiling errors. 


After the middleware(food dresser) gives the okay, the data(food) is dispatched to the reducer(food dispatcher). The reducer takes the data and specifies how the applications state is going to change. The food dispatcher will look at the data(food) that has been provided by the previous action, and changes the state of the empty food tray, to a tray full of delicious tacos. They also leave a ticket that tells the food runner which table the data goes to. The food runner takes this newly acquired state, and brings the delicious tacos to the correct table, or the view of the page. As soon as the customer is done viewing the data and leaves, the server waits for another hungry table to come by, 


Completing the React-Redux project is an amazing feeling, as I am ending my journey as a student of Full-Stack development, and I am beginning to enter a new chapter of my life, where I get to use the knowledge I gained through Flatiron in my professional career. I am one step closer to achieve my career goals, entering a job field that I have a lot of passion for. 

 

