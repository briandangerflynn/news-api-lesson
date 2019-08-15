# news-api-lesson
In this lesson, we're going to review basic HTML, CSS, and JavaScript by building a website that uses the [news api](https://newsapi.org).

## Before We Begin
#### Text Editor
Text Editors are basically like Microsoft Word or Google Docs, except it's for writing code instead of regular text. We're going to use a popular text editor called Visual Studio Code, or VS Code. 

[You can download Visual Studio Code here](https://code.visualstudio.com/). 

#### Web Browser
Web Browsers are how we search the web. You probably know this already because you're not 80 years old, but if you don't, you can just nod and pretend you already knew. We're going to use Google Chrome, cause it's the friggin' best.

If you don't already have it, [you can download Chrome here](https://www.google.com/chrome/b/).

## Front End Vs. Back End Web Development
Put simply, the "front end" of a web application is all the stuff a user can see and interact with on their web browser — AKA the "User Interface."

The "back end" of a web application is essentially the database. It controls what data is rendered on the front end. It also controls any creation or manipulation of data by the actions the user takes on the front end.

For example, the front end of Twitter has a form where you can enter a new Tweet and a button that you can click on when you're done typing your Tweet. The back end of Twitter is the database that stores your new Tweet.

![](http://cdn.differencebetween.net/wp-content/uploads/2018/04/Frontend-VERSUS-Backend.jpg)

People who like front end picture the difference between the two like this:
![](https://i.redd.it/ku1neu504sh01.jpg)

People who like back end might feel differently:
![](https://i.redd.it/lp2qlml2wxl01.jpg)

Whichever way you feel, most programmers begin with front end web development and grow from there, so today's lesson will be entirely front end focused.

#### Clients and Servers
The world wide web is basically just an interconnected network of client devices and servers. 

We use the word **"client"** to refer to a computer connected to the internet that is being used by a human. Clients would include your laptop, your smart phone, your Apple TV, etc. 

![](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c9/Client-server-model.svg/1200px-Client-server-model.svg.png)

A **"server"** is a computer who's primary purpose is just to store data. Humans don't normally interact with a server directly, so they have almost no interface. They often kind of ook like a VCR:

![](https://encrypted-tbn0.gstatic.com/shopping?q=tbn:ANd9GcRBQ6I4NzSHMvx7Wrdyy4BfY-HV1pY5Iji10WFRDs1AxPfvv8BgRoNPCDEM-pLNaRaIwlAr8LPzvS89M5xTKOY6g0aWKjRhNdsuy9zaZ99eWFLgffpM2Il-Zw&usqp=CAc).

You may be more familiar seeing them stacked in a cluster, like this:
![](https://5.imimg.com/data5/FD/SW/MY-37259883/computer-server-500x500.jpg)

## HTTP Requests
Client computers have interfaces with which humans can interact. When people are using such a device to interact with an app, these interactions can be boiled down to four core actions:
- Creating new data
- Reading existing data
- Updating existing data
- Deleting existing data

Apps that allow users to do these four actions are known as CRUD apps.

###### What are examples of each of these 4 CRUD actions on Facebook?

When we perform one of these four CRUD actions, we're making a an HTTP request to a server to fulfill our specified action. HTTP stands for **H**yper**T**ext **T**ransfer **P**rotocol. You can think of HTTP as a set of rules for transferring data over the web. There are four types of HTTP requests that connect with our four user interactions:

- POST request == Create data
- GET request == Read data
- PUT request == Update data
- DELETE request == Delete data (whoa! who knew!?!)

![](https://res.cloudinary.com/briandanger/image/upload/v1558470312/Screen_Shot_2019-05-21_at_4.24.21_PM_jgcf1q.png)

When a user makes one of these requests, the server will "respond" with either a success or error message and by either doing or not doing the action requested. There are a number of factors affecting success that we will discuss at greater length in the future.

We'll need to wait until we learn backend database languages before we can Create, Update, or Delete data from a database; however, fortunately, we can Read existing data with just JavaScript, so for now, we'll focus on how we can us JS to request data from servers that our users can read, watch, and listen to.

## APIs
APIs are basically databases hosted on web servers that have data that is available for public use. This may not sound particularly exciting at first, but APIs are actually one of the most useful tools in web development.

#### API Example - OpenWeatherMap
Imagine you're building a hiking app. You might want to have information about the weather available when your users are planning when and where they're going to hike. Without access to a weather database, providing this information to your users would be nearly impossible. 

Fortunately, we have [the Weather API](https://openweathermap.org/api). When you send an HTTP GET request to this API, it will respond back to you with whatever weather data you requested, allowing you to display that information in your app for your users.

There are LOADS of APIs on the web, ranging from those containing extremely helpful information like the weather, financial data, and government data to those containing really fun info like a database of Jeopardy questions or breweries or Star Wars info.

So, how do we actually use APIs?

## Axios
`Axios` is a very popular JavaScript library you can use to perform HTTP requests. 

Because `axios` is a library, you have to first add it to your project. You can link to the `axios` library in the head section of your HTML page with `<script src="https://unpkg.com/axios/dist/axios.min.js"></script>`. Make sure to place the link to `axios` *before* the link to your main JS document or it won't work.

`Axios` has shorthand methods for all four of our CRUD actions / HTTP request methods:

- you can CREATE with `axios.post()`
- you can READ with `axios.get()` `//<-- we'll be focusing on this one for now`
- you can UPDATE with `axios.put()`
- you can DELETE with `axios.delete()` 

Let's put all this boring lecture stuff into action and actually build an app!

## We Do: Building Our Own News Website!
Open your computer terminal. PLEASE DO NOT TYPE ANY COMMANDS INTO YOUR TERMINAL BEYOND WHAT'S WRITTEN HERE.

We're going to navigate to the desktop by typing `cd Desktop` and hitting `enter`. This stands for "change directory to desktop". 

Here, we're going to make a folder (aka directory) for our news app project  with `mkdir news_app`. You should see this folder appear on your desktop. Then, we're going to move into that folder with `cd news_app`. 

Once inside our news app, we're going to make our three primary files by typing `touch index.html style.css script.js` and hitting `enter`. 

You can shrink your terminal for now. There's a fun reason we used this complicated way of creating a new project... :)

Open VS Code and open your news_api project. It should look like this: 

![](https://res.cloudinary.com/briandanger/image/upload/v1565907352/Screen_Shot_2019-08-15_at_6.15.30_PM_m5zgwh.png)

Let's start with `index.html`

#### HTML
Html provides the content of a page: the text, images, videos, links, etc. Without any CSS, this content will have no style whatsoever. Without any JavaScript, the functionality will be extremely limited.

Copy and paste the following code into your HTML. I'll explain it line by line:

```
<!DOCTYPE html>
<html>
  <head>
    <title>News App</title>
    <link rel="stylesheet" type="text/css" href="css/main.css">
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script defer src="js/main.js"></script>
  </head>

  <body>
    <header>
      <h1>Choose Your News Source</h1>
      <select>
        <option value="abc-news">ABC</option>
        <option value="cbs-news">CBS</option>
        <option value="business-insider">Business Insider</option>
        <option value="espn">ESPN</option>
        <option value="buzzfeed">Buzzfeed</option>
      </select>
      <button type="button" name="button">Select</button>
    </header>

    <div class="articles">

    </div>
  </body>
</html>
```

Save your file and open your code in the browser. It should look like this:
![](https://res.cloudinary.com/briandanger/image/upload/v1565907617/Screen_Shot_2019-08-15_at_6.20.07_PM_buuosk.png)

#### CSS
CSS provides the styles for our apps. Let's sharpen our app up a bit with the following code:

```
body {
  margin:0;
}

header {
  font-family: arial;
  text-align: center;
  background-color: #000033;
  color: white;
  height: 100px;
  padding-top: 50px;
}

h1, h3, p {
  margin: 0;
}

.article {
  display: flex;
  margin-bottom: 20px;
}

.article-image {
  width: 25%;
}

.article-description {
  width: 74%;
  padding-left: 1%;
}

a {
  color: #000033;
}

img {
  width: 100%;
}
```



