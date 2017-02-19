---
layout: post
title: "API Design Best Practices"
date: 2017-02-19 06:39:00 +6390
categories: api
lang: en
ref: api-design-best-practices
---

## **Summary**
The objective of this reference document is to define the best practices and frameworks for developing APIs.

This is a development guide that contains rules and standards to follow in the building of APIs following the best 
practices of design and continuous improvement.

## **Overview**
The API’s job is to make the developer as successful as possible.

The orientation for APIs is to think about design choices from the application developer’s point of view.

The primary design principle when crafting your API should be to maximize developer productivity and success.

A right design communicates how something will be used. The question becomes - what is the design with optimal benefit 
for the app developer?

The developer point of view is the guiding principle for all the specific tips and best practices we’ve compiled.

## **Contents**
1. [Use nouns in order to name a resource](#use-nouns-in-order-to-name-a-resource)
1. [Use plural names and concrete names](#use-plural-names-and-concrete-names)
1. [Simplify associations](#simplify-associations)
1. [Sweep complexity behind the ?](#sweep-complexity-behind-the-?)
1. [Handling errors](#use-parameterized-logging)
1. [Versioning](#provide-useful-event-context)
1. [Pagination](#what-should-you-log)
1. [Partial response](#tune-your-pattern)
1. [Fields parameter syntax summary ](#log-method-arguments-and-return-values)

## **Use nouns in order to name a resource**
The number one principle in pragmatic RESTful design is: keep simple things simple.

Keep the base URL simple and intuitive the base URL is the most important design affordance of your API. A simple and intuitive base URL design makes using your API easy.

Keep verbs out of the base URL

There should be 2 base URL per resource the first URL is for a collection, the second URL is for a specific element in the collection.

Use HTTP verbs to operate on the collection and elements

HTTP verbs are POST, GET, PUT, DELETE

| RESOURCE      | POST         | GET                   | UPDATE                                  | PATCH                                                    | DELETE       |
|---------------|--------------|-----------------------|-----------------------------------------|----------------------------------------------------------|--------------|
| /services     | create new   | get a collection list | bulk, update                            | return error                                             | delete all   |
| /services/100 | return error | get by Id             | if exists then update else return error | if exists then update the fields given else return error | delete by id |

[Go to Contents Table](#contents)

## **Use plural names and concrete names**
Given that the first thing most people probably do with a RESTful API is a GET, we think it reads more easily and is 
more intuitive to use plural nouns. But above all, avoid a mixed model in which you use singular for some resources, 
plural for others. Being consistent allows developers to predict and guess the method calls as they learn to work with 
your API.

**Example:**

| RESOURCE             |
|----------------------|
| /hotels/             |
| /hotels/100/rooms    |
| /hotels/100/rooms/10 |
| /deals               |
| /bookings            |


[Go to Contents Table](#contents)

## **Simplify associations**
Resources almost always have relationships to other resources. What's a simple way to express these relationships in a 
Web API?

For example given the following operations GET /owners/5678/dogs and POST /owners/5678/dogs the relationships can be 
complex. Owners have relationships with veterinarians, who have relationships with dogs, who have relationships with 
food, and so on. It's not uncommon to see people string these together making a URL 5 or 6 levels deep.

**_Once you have the primary key for one level, you usually don't need to include the levels above because you've already 
got your specific object._**

[Go to Contents Table](#contents)

## **Sweep complexity behind the ?**

Make it simple for developers to use the base URL by putting optional states and attributes behind the HTTP question mark.

For example to get all red dogs running in the park: **_GET /dogs?color=red&state=running&location=park_**

[Go to Contents Table](#contents)

## **Handling errors**
Error handling it is a very important piece of the puzzle for any software developer, and especially for API designers.

### **Use HTTP status codes**
Use HTTP status codes and try to map them cleanly to relevant standard-based codes.

| STATUS CODE | DESCRIPTION                                                                                                                                                                                                                                                                                                            |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | OK Standard response for successful HTTP requests. The actual response will depend on the request method used. In a GET request, the response will contain an entity corresponding to the requested resource. In a POST request, the response will contain an entity describing or containing the result of the action |
| 201         | Created The request has been fulfilled, resulting in the creation of a new resource                                                                                                                                                                                                                                    |
| 304         | Not Modified Indicates that the resource has not been modified since the version specified by the request headers If-Modified-Since or If-None-Match. In such case, there is no need to retransmit the resource since the client still has a previously-downloaded copy.                                               |
| 400         | Bad Request The server cannot or will not process the request due to an apparent client error (e.g., malformed request syntax, too large size, invalid request message framing, or deceptive request routing)                                                                                                          |
| 401         | Unauthorized Similar to 403 Forbidden, but specifically for use when authentication is required and has failed or has not yet been provided. The response must include a WWW-Authenticate header field containing a challenge applicable to the requested resource                                                     |
| 403         | Forbidden The request was a valid request, but the server is refusing to respond to it. The user might be logged in but does not have the necessary permissions for the resource.                                                                                                                                      |
| 404         | Not Found The requested resource could not be found but may be available in the future. Subsequent requests by the client are permissible                                                                                                                                                                              |
| 500         | Internal Server Error A generic error message, given when an unexpected condition was encountered and no more specific message is suitable                                                                                                                                                                             |

### **The error message payload and the header should include the following attributes**
* The status code in the response header
* The status code in the payload
* The developer error message in the payload
* The user error message in the payload
* The error code in the payload
* The link in order to give a more deep information about the error in the payload

**Example**

```json
HTTP Status Code: 401
{
    "status" : "401", 
    "developerMessage":"A developer message",
    "userMessage":"A user message",
    "errorCode": 20003, 
    "moreInfo": "http://www.myawesomeapi.com/docs/errors/20003"
}
```

[Go to Contents Table](#contents)

## **Versioning**
Versioning is one of the most important considerations when designing your Web API.

Never release an API without a version. Make the version mandatory.

Specify the version with a ‘v’ (e.g. v1).

Use a simple ordinal number. Don’t use the dot notation like v1.2 because it implies a granularity of versioning that 
doesn’t work well with APIs--it’s an interface not an implementation. Stick with v1, v2, and so on.

### **Use the Accept Header**
There is a well-known HTTP header called Accept which is sent on a request from a client to a server. For instance

Accept: application/json

This notation is saying that I, the client, would like the response to be in json please.

The accept headers is using this header to make up your own resource types, for example:

Accept: application/vnd.myapi.v2 + json

**_Using headers is more correct for many reasons: it leverages existing HTTP standards, it’s intellectually consistent 
with Fielding’s vision, it solves some hard real-world problems related to inter-dependent APIs, and more._**

**_Example_**

```xml
http://company.com/api/customer/123
===>
GET /customer/123 HTTP/1.1
Accept: application/vnd.company.myapp.customer-v3+xml
 
<===
HTTP/1.1 200 OK
Content-Type: application/vnd.company.myapp-v3+xml
<customer>
  <name>Neil Armstrong</name>
</customer>
```

[Go to Contents Table](#contents)

## **Pagination**
* Make it easy for developers to paginate objects in a database
* It’s almost always a bad idea to return every resource in a database.
* Use limit and offset. It is more common, well understood in leading databases, and easy for developers. 
**/dogs?limit=25&offset=50**
* We also suggest including metadata with each response that is paginated that indicated to the developer the total number
of records available.

[Go to Contents Table](#contents)

## **Partial response**
Partial response allows you to give developers just the information they need.
Take for example a request for a tweet on the Twitter API. You’ll get much more than a typical twitter app often needs 
including the name of person, the text of the tweet, a timestamp, how often the message was re-tweeted, and a lot of 
metadata.

See google approach https://developers.google.com/+/web/api/rest/

By default, the server sends back the full representation of a resource after processing requests. For better performance,
you can ask the server to send only the fields you really need and get a partial response instead.

To request a partial response, use the fields request parameter to specify the fields you want returned. 
You can use this parameter with any request that returns a response body.

**Example**

The following example shows the use of the fields parameter with the Google+ API.

**Simple request:** This HTTP GET request omits the fields parameter and returns the full activity resource, with its 
dozens of fields.

**https://www.googleapis.com/plus/v1/activities/z12gtjhq3qn2xxl2o224exwiqruvtda0i?key=YOUR-API-KEY**

**Request for a partial response:** This HTTP GET request for the above resource that uses the fields parameter 
significantly reduces the amount of data returned.

**https://www.googleapis.com/plus/v1/activities/z12gtjhq3qn2xxl2o224exwiqruvtda0i?fields=url,object(content,attachments/url)&key=YOUR-API-KEY**

In response to the above request, the server sends back a JSON response that contains only the url field and the pared-down 
object that includes only content and attachments.url.

```json
{
 "url": "https://plus.google.com/102817283354809142195/posts/F97fqZwJESL",
 "object": {
  "content": "A picture... of a space ship... launched from earth 40 years ago.",
  "attachments": [
   {
    "url": "http://apod.nasa.gov/apod/ap110908.html"
   }
  ]
 }
}
```
Note that the response is a JSON object that includes only the selected fields and their enclosing parent objects.

Syntax of the fields parameter is covered next, followed by more detail about what gets returned in the response.

### **Fields parameter syntax summary**
The format of the fields request parameter value is loosely based on XPath syntax. The supported syntax is summarized below

* Use a comma-separated list to select multiple fields.
* Use a/b to select a field b that is nested within field a; use a/b/c to select a field c nested within b.
* Specify field sub-selectors to request only specific sub-fields by placing expressions in parentheses "( )" after any 
selected field. ( For example: fields=items(id,object/content) returns only the item id and object's content, for each 
items array element. )
* Use wildcards in field selections, if needed. ( For example: fields=items/object/* selects all items in an object. )


`Here are some collection-level examples from activities.list:
`

|  Examples      |  Effect                                                                                                                                                                                                                                                      |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| items          | Returns all elements in the items array, including all fields in each element, but no other fields.                                                                                                                                                          |
| items/title    | Returns only the title field for all elements in the items array. Whenever a nested field is returned, the response includes the enclosing parent objects. The parent fields do not include any other child fields unless they are also selected explicitly. |
| updated, items | Returns both the updated field and all elements in the items array.                                                                                                                                                                                          |


`Here are some resource-level examples from activities:
`

| Examples               | Effect                                                                                                               |
|------------------------|----------------------------------------------------------------------------------------------------------------------|
| title                  | Returns the title field of the requested resource.                                                                   |
| actor/displayName      | Returns the displayName sub-field of the actor object in the requested resource.                                     |
| object/attachments/url | Returns only the url field for all members of the attachments array, which is itself nested under the object object. |


`Field sub-selections: Request only parts of the selected elements.
`

By default, if your request specifies particular objects, the server returns the objects in their entirety. You can specify 
a response that includes only certain sub-fields within the selected objects. You do this using "( )" sub-selection syntax, 
as in the example below:


| Example       | Effect                                                                                |
|---------------|---------------------------------------------------------------------------------------|
| items(id,url) | Returns only the values of the id and url fields for each element in the items array. |


[Go to Contents Table](#contents)

## **Handling partial responses**

[Go to Contents Table](#contents)

## **Responses that don’t involve resources**

### **Use verbs not nouns**

[Go to Contents Table](#contents)

## **Supporting multiple formats**

[Go to Contents Table](#contents)

## **Attribute names**

[Go to Contents Table](#contents)

## **Tips for search**

[Go to Contents Table](#contents)

## **Resources**

[Go to Contents Table](#contents)
