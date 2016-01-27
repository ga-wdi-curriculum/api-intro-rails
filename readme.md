# How to Work With and Build APIs

![](http://washingtontechnology.org/wp-content/uploads/2014/11/General_Assembly_logo.png)

## Introduction to APIs

### Installfest

Tools needed for today’s class:
- [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git#Installing-on-Mac)
- [homebrew (mac only)](http://brew.sh)
- [mongodb](https://docs.mongodb.org/v3.0/tutorial/install-mongodb-on-os-x/#id3)
- node and npm
  - `brew install node`
  - `brew install npm`

### What's an API?

- API is an acronym for Application Programming Interface
- An API is a service that provides raw data for public use
- Application programming interface technically applies to all of software design
- Term API evolved to define specifically URLs that allow the user to access raw data
- APIs publish data for public use
- As third-party software developers, we can access an organization’s API and use their data in our applications

A couple examples - stock quotes
http://dev.markitondemand.com/MODApis/Api/Quote/json?symbol=AAPL
http://dev.markitondemand.com/MODApis/Api/Quote/json?symbol=GOOGL

To format the output in your browser, install this chrome extension: https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc?hl=en

### Types of serialized data

#### JSON
JavaScript Object Notation
Universal standard for serializing native data structures for transmission
Lightweight
Easy to read
JSON needs to be parsed before we can use it

#### XML
eXstensible Markup Language
Granddaddy of serialized data formats
Based on HTML
Cumbersome to parse
Frequent legacy use
You’ll probably favor using a JSON API, if it’s available

Same API, different formats
Many APIs publish data in different formats, such as:
http://dev.markitondemand.com/Api/Quote/json?symbol=AAPL
http://dev.markitondemand.com/Api/Quote/xml?symbol=AAPL

### We do: A close look at an API request with Postman
Let’s make a basic HTTP request to an API
We can do this in the browser, but let’s use Postman to take a detailed look
What is Postman?
A Chrome extension for making HTTP requests 

### You do: Talk with the Postman
- Download Postman
- Go to https://www.getpostman.com/
- Open the app
- Type the URL of an API call 
- Ensure the method is GET
- Click Send

| API | Sample URL |
|-----|------------|
| **[This for That](http://itsthisforthat.com/)** | http://itsthisforthat.com/api.php?json |
| **[iTunes](https://www.apple.com/itunes/affiliates/resources/documentation/itunes-store-web-service-search-api.html)** | http://itunes.apple.com/search?term=adele |
| **[Giphy](https://github.com/Giphy/GiphyAPI)** | http://api.giphy.com/v1/gifs/search?q=funny+cat&api_key=dc6zaTOxFJmzC |
| **[OMDB API](http://www.omdbapi.com/)** | http://www.omdbapi.com/?t=Game%20of%20Thrones&Season=1 |
| **[StarWars](http://swapi.co/)** | http://swapi.co/api/people/3 |
| **[Stocks](http://dev.markitondemand.com/MODApis/)** | http://dev.markitondemand.com/Api/Quote/json?symbol=AAPL |

### How do we identify resources?

- Uniform Resource Identifier (URI) is a string of characters that identifies the name of a resource
- The most common URI is the Universal Resource Locator (URL) or web address
- The URL goes a step farther than the URI and specifies the means of accessing the resource (HTTP)
- There are two primary uses for APIs

### Programmatically accessing data

#### What is HTTP?
- HTTP stands for Hypertext Transfer Protocol
- Hypertext is text displayed on an electronic device with links to other text
- Underlying protocol for data exchange on the World Wide Web

#### How does HTTP work?	
- HTTP is a client-server protocol
- A client-server protocol divides tasks between the server, the resource provider, and the client, the resource requestor
- HTTP is a request-response protocol
- The client requests data and the server responds to the request
- HTTP works through request methods, also called HTTP verbs
- HTTP verbs describe the action you want to do on the desired resource

#### HTTP verbs

| Method | Description |
| --- | --- |
| GET | requests a representation of the specified resource, only retrieves data |
| POST | requests that the server accept the data enclosed in the request as a new subordinate of the resource the URI identifies |
| PUT | requests the enclosed entity be stored under the supplied URI |
| DELETE | deletes the selected resource |

- HTTP is stateless
- HTTP treats each request as an independent transaction that is unrelated to any previous request
- The communication consists of independent pairs of request and response
- You can understand each request message in isolation

#### What is REST?

- REST stands for Representational State Transfer
- REST is an architectural style for designing networked applications
- RESTful applications use HTTP requests to post data, read data and delete data
- The World Wide Web is itself a gigantic RESTful application

#### How does REST work?
- REST tries to keep things as simple as possible
- Uses HTTP request methods as a resource interface
- REST uses HTTP methods to perform create, read, update, and delete (CRUD)

| Method | CRUD Action |
| --- | --- |
| GET | Read |
| POST | Create |
| PUT | Update|
| DELETE | Delete |

### 3rd party authentication

## What is OAuth?

You see many sites with buttons that allow for users to sign up with their Facebook or Twitter credentials.  OAuth makes all this possible.  

[OAuth](https://en.wikipedia.org/wiki/OAuth) is an agreed-upon set of standards for logging in through a third party service. It involves:

1. Leaving a website.
2. Authenticating with the third party.
3. Then the third party will redirect the user back to the original website with, among other things, an authentication token that can be persisted and used to request more information later.  

At a high level, the standard lays out the overall protocol of login: you have to have _this_ route in your application, with _these_ parameters in your request/response, and after that, you need to be directed to _these_ pages.  And because it's a set of standards that are universally accepted, there's a whole bunch of libraries we can use to make this happen - like [Passport](http://passportjs.org/)!

![facebook-login](https://cloud.githubusercontent.com/assets/40461/9360397/e49b15be-468d-11e5-8b88-3757ca6cbcac.png)

You probably know this as "Login with Facebook": you click on "Login with Facebook", you're redirected to Facebook's application, and then you get back to your site.

## Turn & Talk: Local vs. 3rd Party User Authentication

What are the pros and cons of authenticating users locally (plain ol' username and password) or via a 3rd party application (like Twitter or Facebook).

> As a developer, one benefit is that you don't have to worry about developing your own authentication system.  The other benefit is your application gets a whole bunch of information it can use - or persist - later on, from Facebook.  A downside for the users is that in order to login, they're giving a lot of of their data to the requesting application. Developers and companies love this, though, because they can use all this data from the OAuth provider (Facebook/Twitter etc).

#### What information is available via OAuth?

Here's part of a sample response from Twitter. There's plenty more information that is cut off here for readability.

```js
{
  id: '8839212',
  username: 'urdmaseda',
  displayName: 'Adrian Maseda',
  photos: [ { value: 'https://pbs.twimg.com/profile_images/609055940596236288/RfQHyuDo_normal.jpg' } ],
  provider: 'twitter',
  _json:
   { id: 8839212,
     id_str: '8839212',
     name: 'Adrian Maseda',
     screen_name: 'urdmaseda',
     location: 'DC',
     profile_location: null,
     description: 'WDI Instructor @GA_DC // Founder @AllThingsGo',
     url: 'http://t.co/WVMZNQNlM7',
     entities: { url: [Object], description: [Object] },
     protected: false,
     followers_count: 501,
     friends_count: 641,
     listed_count: 20,
     created_at: 'Wed Sep 12 18:56:55 +0000 2007',
     favourites_count: 667,
     utc_offset: -18000,
     time_zone: 'Eastern Time (US & Canada)',
     geo_enabled: false,
     verified: false,
     statuses_count: 2157,
     lang: 'en',
  }
}
```

#### How it works

To make any of our apps work, we need to first declare our app as a Twitter application using Twitter's [developer interface](https://apps.twitter.com/).  Ultimately, we'll be defining the set of permissions / information we are requesting from the user.

A visitor of our website clicks **Login with Twitter**, and leaves our original application and are brought to Twitter - as a developer, you lose everything you had (params from a form, for example).  

As a Twitter user, when you login, you pass in two important pieces of information to Twitter: the **app ID** and the **app secret** that identifies the application requesting the information.  

After our app is given the okay, Twitter sends back an **access token**. With that access token, Twitter can identify users of our application as real Twitter users. These access tokens only last so long, usually expiring after a week or so, but with this access token we can call out to Twitter, if we want, and get Twitter data associated with that Twitter user.

> You'll be able to see this access token via the callback URL in the browser. It will look something like `/auth/twitter/callback?oauth_token=_emExwAAAAAAjDpMAAABUXmEXAg&oauth_verifier=e9g1zE58fJGz1K3FJklSqg0GG5OTNDE0`

## Working with APIs

Let's build a weather app CLI that tells us the weather given any zipcode.

[Starter Code](https://github.com/ga-dc/node-cli-weather) | [Solution Code](https://github.com/ga-dc/node-cli-weather/tree/solution)

### Initial Setup

    $ git clone https://github.com/ga-dc/node-cli-weather
    $ cd node-cli-weather
    $ npm install

- Visit http://www.wunderground.com/weather/api/d/login.html and create a free account.
- Click "Explore My Options"
- Click "Purchase Key"
- Visit http://www.wunderground.com/weather/api/d/docs and click "Show Response"

```js
// env.js
module.exports = {
  wuApiKey: "Your API Key Here"
}
```

### Looking up an area by zipcode

```js
// app.js

var env = require("./env");
var zipcode = 20002;
var apiUrl = "http://api.wunderground.com/api/" + env.wuApiKey;
var url = apiUrl + "/geolookup/q/" + zipcode + ".json";

console.log(url);
```

View this url in the browser.

### Request that json from node

```js
// app.js
...
var request = require("request");
request(url, function(err, response, body){
  console.log(response);
})
```

### Get the conditions API endpoint

```js
// app.js
...
request(url, function(err, response, body){
  var location = JSON.parse(body).location.requesturl;
  var url = apiUrl + "/conditions/q/"+location+".json";
  console.log(url);
})
```

View this url in the browser.

### Request that json from node

```js
// app.js
...
var apiUrl ="http://api.wunderground.com/api/"+env.wuApiKey;
var url = apiUrl + "/geolookup/q/"+zipcode+".json";
request(url, function(err,res,body){
  var location = JSON.parse(body).location.requesturl;
  var url = apiUrl + "/conditions/q/"+location+".json";
  request(url, function(err,res,body){
    var observation = JSON.parse(body).current_observation
    console.log("The weather in", observation.display_location.full, "is", observation.weather)
  })
})
```

## Build Your Own API

[Starter Code](https://github.com/ga-dc/products-api) | [Solution Code](https://github.com/ga-dc/products-api/tree/solution)

### Express

[Express.js](http://expressjs.com/en/index.html) is a web framework for node js.

    $ mkdir products-api
    $ cd products-api
    $ npm init
    $ npm install --save express

```js
// index.js

var express = require("express");
var app = express();
app.get("/", function(req, res){
  res.send("hello world");
})
```

Next, let's hardcode some data and respond with json

```js
// index.js

var products = [
  "Lip Balm Set organic lip balm stocking stuffers Natural lip balm Pick 3",
  "Purple and Gray dreamy bird ornament - Beautiful Bird decoration in beige - Upcycled Woodland hanging"
];

app.get("/products",function(req, res){
  res.json(products);
});
```

And a show route

```js
// index.js

app.get("/products/:id", function(req, res){
  var product = products[req.params.id];
  res.json(product);
});
```

>Bonus! Try adding create and delete functionality.

Hint: use `.post` and `.delete` methods

### MongoDB

When compared to relational databases, NoSQL databases are more scalable and provide superior performance, and their data model addresses several issues that the relational model is not designed to address:

- Large volumes of rapidly changing structured, semi-structured, and unstructured data
- Agile sprints, quick schema iteration, and frequent code pushes
- Object-oriented programming that is easy to use and flexible
- Geographically distributed scale-out architecture instead of expensive, monolithic architecture

A record in MongoDB is a document, which is a data structure composed of field and value pairs. MongoDB documents are similar to JSON objects. The values of fields may include other documents, arrays, and arrays of documents.

#### Mongoose

Mongoose is a node module that simplifies interacting with the mongo database. We'll use it to define
a product model and query the database.

#### Seed the Database

Make sure mongo is running: `$ mongod`

```js
// seeds.js

var mongoose = require("mongoose");
mongoose.connect("mongodb://localhost/products");
var Product = mongoose.model("Product",{
  title: String,
  price: Number,
  category: String
})
Product.remove({}, function(){
  Product.create(
    {title: "Cards Against Humanity", price: 25.00, category: "Toys & Games"}, 
    {title: "Pie Face Game", price: 25.36, category: "Toys & Games"},
    {title: "Fire, 7\" Display, Wi-Fi, 8 GB - Includes Special Offers, Black", price: 44.99, category: "Electronics"},
    {title: "Amazon Echo", price: 179.99, category: "Electronics"},
    {title: "Fujifilm Instax Mini Instant Film, 10 Sheets x 5 packs ", price: 41.90, category: "Camera & Photo"},
    function(err, products){
      console.log(products);
      process.exit();
    }
  );
});
```

#### Query the DB from Express

```js
// app.js

app.get("/products", function(req, res){
  Product.find({}, function(err, products){
    res.json(products); 
  })
})
```

#### You do: Modify the show route to find a product by ID

Hint: http://mongoosejs.com/docs/api.html#model_Model.findById

You can access the id from the URL using `req.params.id`.

#### We do: Create

    $ npm install --save body-parser

```js
// app.js

var bodyParser = require("body-parser");
app.use(bodyParser.urlencoded());
app.post("/products", function(req, res){
  Product.create(req.body, function(err, product){
    res.json(product);
  })
})
```

#### We do: Update

```js
// app.js

app.patch("/products/:id", function(req, res){
  Product.findByIdAndUpdate(req.params.id, req.body, function(err, product){
    res.json(product);
  })
})
```

#### You do: Delete

Hint: http://mongoosejs.com/docs/api.html#model_Model.findByIdAndRemove
