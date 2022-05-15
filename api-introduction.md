## What is an API?

Application Program interface. It serves as the interaction layer between a requesting service and a requestor, typically on the Web.

## What is a REST API?

REST = Representational State Transfer. It's a style of API and not a standard. REST APIs rely on HTTP to deliver requests from a requestor in order to return a response to the requestor.

Typically, the vehicle for this exchange is a JSON file, favored for being lightweight and thus preferred for speed. However, any data format can be used for the API request-response

## How do rest APIs differ from other types of APIs?

There are native APIs, which rely on language-specific designs. Web APIs, of which REST APIs are one type, are language-agnostic.

Besides REST APIs, the other main kind of web APIs are SOAP (Simple Object Access Protocols) APIs.
The main differences are structure and speed. SOAPs rely on a highly structured XML request and response. This makes them slow. 

SOAPs are now primarily involved in legacy systems and in highly regulated industries, like finance. 

## What is an endpoint?

An endpoint is simply one end of the communication channel. Each endpoint is the location from which APIs can access the resources they need to carry out their function.

### Breaking Down a Sample Endpoint

Sample: 

```
http://apiserver.com/homes?limit=5&format=json
```
The whole thing is officially an endpoint, but the *documentation* breaks this down into three different components:

 - the base path: Above, the `http://apiserver.com`
 - the endpoint: Above, the `/homes`
 - the query string parameters: Above, the `?limit=5&format=json`

## Why does documentation matter with REST APIs?

To understand how to interact with a REST API, you have to read the documentation for the API. The need to read the docs makes the technical writer’s role extremely important with REST APIs.

However, because *some* portions of API documentation can be automated, many companies do not invest in technical writers. They automate and then expect the developers to make up any gap left by the automated piece.

## What is the market for API documentation?

Surprisingly, the market is hot, despite the fact that many companies are not investing in a technical writing staff.

That's because writing the reference docs for an API is only half the battle. As you are writing for developers who are interacting with the APIs programmatically, the docs are essentially the main interface for a developer-user. So, the presentation of the content matters as much as the text itself.








