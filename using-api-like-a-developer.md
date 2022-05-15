# Using an API Like a Developer

## Example problem and questions

Looking at the [Open Weather API documentation](https://openweathermap.org/current):

- Does the API provide the information we need about temperature, wind speed, wind direction, and current conditions?

  - Yes, separate nested keys for "main", "wind", "weather"
  
- How many different ways can you specify the location for the weather information?

  - One, I think? Only accepts latitude and longitude coordinates
  
- What does a sample request look like?

```json
{
  "coord": {
    "lon": 139,
    "lat": 35
  },
  "weather": [
    {
      "id": 800,
      "main": "Clear",
      "description": "clear sky",
      "icon": "01n"
    }
  ],
  "base": "stations",
  "main": {
    "temp": 283.88,
    "feels_like": 282.52,
    "temp_min": 283.88,
    "temp_max": 283.88,
    "pressure": 1011,
    "humidity": 58
  },
  "visibility": 10000,
  "wind": {
    "speed": 2.76,
    "deg": 58,
    "gust": 5.14
  },
  "clouds": {
    "all": 0
  },
  "dt": 1647357046,
  "sys": {
    "type": 2,
    "id": 2019346,
    "country": "JP",
    "sunrise": 1647377649,
    "sunset": 1647420692
  },
  "timezone": 32400,
  "id": 1851632,
  "name": "Shuzenji",
  "cod": 200
}
```                          

- How many endpoints does the API have?

  - Not really sure?
  
- What authorization credentials are required to get a response?

  - Nothing?


## API Features

### Authorization Keys

Authorization keys allow API publishers to license access to the API, rate limit the number of requests, control access over the API, etc.

## Testing APIs

Testing APIs can be done via the command line with curl or via a web-based GUI platform like Postman.

### Using Postman to make a request to OpenWeather current weather API

1. Open Postman app.
2. Create a new request.
3. List the following in the GET field: https://api.openweathermap.org/data/2.5/
4. Fill out the params fields with various key-value pairs
5. Click 'send'.

## Using Curl

curl (or cURL) is a command-line utility that can be used to make requests to an API or a website.

For example:

```sh
curl -X GET "https://api.openweathermap.org/data/2.5/weather?zip=95050&appid=b004cf0d4ae72210092330426d65ea79&units=imperial"
```
returns the following:

```json
{"coord":{"lon":-121.953,"lat":37.3492},"weather":[{"id":801,"main":"Clouds","description":"few clouds","icon":"02d"}],"base":"stations","main":{"temp":80.35,"feels_like":80.35,"temp_min":68.99,"temp_max":87.93,"pressure":1017,"humidity":42},"visibility":10000,"wind":{"speed":14.97,"deg":320},"clouds":{"all":20},"dt":1652559829,"sys":{"type":1,"id":5845,"country":"US","sunrise":1652533187,"sunset":1652584121},"timezone":-25200,"id":0,"name":"Santa Clara","cod":200}
```

You can use Postman to develop code snippets (including for curl) based on the fields you've entered in the GUI.

```sh
curl --location --request GET 'https://api.openweathermap.org/data/2.5/weather?zip=95050&units=imperial&appid=APIKEY'
```

## More on curl

While most programming languages can interact with APIs directly, people like to use curl because it's language agnostic.

You can use curl to get the underlying html from a webpage:

```sh
curl http://www.google.com
```

Append `-i` to the curl request to get the header as part of the respone. Append `I` to see *only* the header in the response.

### curl methods

By default, curl understands the above as a `GET` request unless otherwise specifed. There are four primary methods that you can use in the HTTP protocol:

- POST  = Create a resource
- GET   = read a resource
- PUT   = update a resource
- DELETE = delete a resouce

When specifying a method in curl, begin with the `-X` parameter:

```sh
curl -X GET 
```

### Query Strings

After the endpoint comes the query strings. The start of the query string is signified by the `?`.

```sh
?zip=95050&appid=APIKEY&units=imperial
```

### Common Curl Commands

command|Description|Example|
|------|-----------|-------|
|`-i` or `--incude`|Includes the response headers in the response|`curl -i http://www.example.com`|
|`d` or `--data`|Includes data to post to the URL|`curl -d "data-to-post" http://www.example.com`|
|`-H` or `--header`|Submits the request header to the resource. Headers are common with REST API requests because the authorization is usually included in the header.|`curl -H "key:12345" http://www.example.com`|
|`-X POST`| Specifies the HTTP method to use with the request (in this example, `POST`). If you use `-d` in the request, curl automatically specifies a `POST` method. With `GET` requests, including the HTTP method is optional, because `GET` is the default method used.|`curl -X POST -d "resource-to-update" http://www.example.com`|
|`@filename`|Loads to content from a file.|`curl -X POST -d @mypet.json http://www.example.com`|

### Combining Curl Commands

Like  other command line programs, curl can combine commands:

```sh
curl -i -H "Accept: application/json" -X POST -d "{status:MIA}" http://personsreport.com/status/person123
```

## Example Using Curl Methods

Working on the [Swagger Petstore API](https://petstore.swagger.io/).

### Creating a New Pet 

1. Store the following in a json:

```json
{
  "id": 49,
  "category": {
    "id": 49,
    "name": "test"
  },
  "name": "doggy",
  "photoUrls": [
    "string"
  ],
  "tags": [
    {
      "id": 0,
      "name": "string"
    }
  ],
  "status": "available"
}
```
2. While working in the directory with `pet.json` (file above), run the following:

```sh
curl -X POST --header "Content-Type: application/json" --header "Accept: application/json" -d @pet.json "https://petstore.swagger.io/v2/pet"
```
The `@file` passes the `pet.json` as part of the request to the API.

The `Content-Type` header indicates the type of content submitted in the request body. The `Accept` header indicates the type of content we will accept in the response.

### Update pet

Uses the `POST` method:

1. Change the pet name in the `pet.json`
2. Run the following:

```sh
curl -X PUT --header "Content-Type: application/json" --header "Accept: application/json" -d @pet.json "https://petstore.swagger.io/v2/pet"
```

### Get Pet's Name By ID

1. Pull ID from the `pet.json`
2. Run the following:

```sh
curl -X GET --header "Accept: application/json" "https://petstore.swagger.io/v2/pet/49"
```

### Delete Pet

```sh
curl -X DELETE --header "Accept: application/json" "https://petstore.swagger.io/v2/pet/49"
```

## Idempotency

"A request method is considered “idempotent” if the intended effect on the server of multiple identical requests with that method is the same as the effect for a single such request. Of the request methods defined by this specification, PUT, DELETE, and safe request methods are idempotent”

In other words, with idempotent methods, you can run them multiple times without multiplying the results. 

`GET`, `PUT`, and `DELETE` are idempotent. `POST` is not.


## JSON in API Requests/Responses

JSON is the most typical format for API requests/responses.

Two basic structures in JSON: objects and arrays.

  - Object = collection of key-value pairs, denoted by curly braces.
  - Array = list of items, denoted by square brackets.

Objects can contain arrays, and vice versa

## Accessing Values from Response JSON with Javascript

The following is an example of a webpage with an API call and response embedded. The call is made within the `<script>` tags. Certain parts of the response are then stored as variables and cited within the body of the webpage.

```html
<html>
   <meta charset="UTF-8">
   <head>
      <title>Columbus Weather</title>
      <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>
      <script>
         var settings = {
            "url": "https://api.openweathermap.org/data/2.5/weather?zip=43214&units=imperial&appid=b004cf0d4ae72210092330426d65ea79",
            "method": "GET",
            "timeout": 0,
         };
         
         $.ajax(settings).done(function (response) {
            console.log(response);
            var content = response.wind.speed;
            $("#windSpeed").append(content);
            var speed = response.main.temp;
            $("#temp").append(speed);
            var longitude = response.coord.lon;
            $("#long").append(longitude);
            var latitude = response.coord.lat;
            $("#lat").append(latitude);
         });
         
      </script>
   </head>
   <body>
      <h1>Columbus Current Weather</h1>
      City Coordinates: Longitude: <span id="long"></span>, Latitude: <span id="lat"></span>  </br>
      <br />
      Wind speed:  <span id="windSpeed"></span>  mph</br>
      <br />
      Temperature: <span id="temp"></span> degrees Fahrenheit
      
   </body>
</html>
```

### Dot Notation

Specific values from the JSON response are accessed with dot notation. Follows this format:

RESPONSE.object.key

It's similar for accessing values from arrays, except you use indices, too. For example, imagine we want to get the `main` from the following JSON response:

```json
{
  "weather": [
    {
      "id": 801,
      "main": "Clouds",
      "description": "few clouds",
      "icon": "02d"
    }
  ]
]
}
```
There is only one array here, and under JS, indexing starts at 0. So, to get `main` we want the dot notation

```sh
response.weather[0].main
```


