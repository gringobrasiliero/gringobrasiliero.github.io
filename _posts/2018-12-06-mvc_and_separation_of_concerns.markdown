---
layout: post
title:      "MVC and Separation of Concerns"
date:       2018-12-06 12:17:04 +0000
permalink:  mvc_and_separation_of_concerns
---


When we are creating a web application, we could put all of our lines of code all into one file. We would be able to run the entire application, however, it would be very difficult to debug, and nobody would want to read your code. It would be very difficult to navigate through. It is much better to organize your code into a MVC paradigm, which stands for Model – View – Controller.

Models provide the logic of the application, which is where the data is manipulated and saved. This is also where you can add validations to your forms, and set up relationships between models. In a Mexican restaurant, the cooks would be the Models as they are the ones who make the food. They take orders and prepare the customers meal. Once it is ready, they return it back to the waiter to give back to the customer. 

Views includes all of the front end code (HTML, CSS, JavaScript) of the application, or what the user will see when they open your application. The front end of the restaurant would be the views. You see all the tables, the menus, and hear the authentic music being played on guitars.  

Controllers are the middle-men of the models and views. They relay data from the browser to the application, and from the application to the browser. Controllers are the waiters of the restaurant as they relay information and orders from the users, take the orders to the models, and return tacos back to the customer. 

## Separation of concerns

In a restaurant, we have the dining area, the kitchen staff, and the waiters. For the “Taco Loco” to run effectively, each member of the team has to know and perform their duty. We can not have waiters cooking food, chefs taking orders, and customers in the dining area shouting orders to the chefs in the back. This would cause the restaurant to have a big “problema”, as well as some 1-star reviews. Like a restaurant, we need to make sure that our views only serve as the view that the users see, the models handle the data manipulation and creation, and the controllers bring data back and forth from the view to the model and vice versa. Without keeping this in mind, your web application will become spaghetti code, and this is NOT an Italian restaurant. It will not be organized, having it to where other people will have a harder time contributing to the application, and it will be easy to get lost. 

Making sure to have a separation of concerns will help you keep organized with your code, and it will be much easier to debug, work with others, and have your code running effectively. 


