##Basics

Welcome to SynergyKit's API documentation. We have created a simple namespaced API that allows you full control over your applications.

All of the functionality that you find in our web control panel is available via the API. Today we support all of the major application actions allowing you to build your own control interface using our API.

### Quick reference
All API access is over HTTPS, and accessed via the domain `https://tenant.api.synergykit.com/v2.1` The relative path prefix **/v2.1** indicates that we are currently using version 2.1 of the API.

|Endpoint|HTTP Request|Description
|:-|:-|:-
|**Documents**|||
|`/data/<collectionName>`|POST|<a href="#create-a-new-document">Create a new document</a>
|`/data/<collectionName>/<documentId>`|GET|<a href="#retrieve-an-existing-document-by-id">Retrieve an existing document by ID</a>
|`/data/<collectionName>/<documentId>`|PUT|<a href="#update-document">Update document</a>
|`/data/<collectionName>/<documentId>`|DELETE|<a href="#delete-document">Delete document</a>
|**Users**|||
|`/users`|POST|<a href="#create-a-new-user">Create a new user</a>
|`/users/login`|POST|<a href="#login-user">Login user</a>
|`/users/<userId>`|GET|<a href="#retrieve-an-existing-user-by-id">Retrieve an existing user by ID</a>
|`/users/<userId>`|PUT|<a href="#update-user">Update user</a>
|`/users/<userId>`|DELETE|<a href="#delete-user">Delete user</a>
|`/users/<userId>/roles`|POST|<a href="#add-role">Add role</a>
|`/users/<userId>/roles/<roleUrl>`|DELETE|<a href="#remove-role">Remove role</a>
|`/users/<userId>/platforms`|POST|<a href="#add-platform-to-user">Add platform to user</a>
|`/users/<userId>/platforms/<platformId>`|GET|<a href="#retrieve-platform">Retrieve platform</a>
|`/users/<userId>/platforms/<platformId>`|PUT|<a href="#update-platform">Update platform</a>
|`/users/<userId>/platforms/<platformId>`|DELETE|<a href="#delete-platform">Delete platform</a>
|`/users`|POST|<a href="#linking-users">Linking users</a>
|**Communication**|||
|`/users/notification`|POST|<a href="#send-notification">Send notification</a>
|`/mail/<templateUrl>`|POST|<a href="#send-e-mail">Send e-mail</a>
|**Files**|||
|`/files`|POST|<a href="#upload-file">Upload file</a>
|`/files/<fileId>`|GET|<a href="#retrieve-file-by-id">Retrieve file by ID</a>
|`/files/<fileId>`|DELETE|<a href="#delete-file">Delete file</a>
|**Cloud Code**|||
|`/functions/<cloudCodeUrl>`|POST|<a href="#run-cloud-code">Run cloud code</a>
|**Batch**|||
|`/batch`|POST|<a href="#using-batch">Using batch</a>

###Requests
Any tool that is fluent in HTTP can communicate with the API simply by requesting the correct URI. Requests should be made using the HTTPS protocol so that traffic is encrypted. The interface responds to different methods depending on the action required. Whole API is based on CRUD principles.

For POST and PUT requests, the request body must be JSON, with the Content-Type header set to application/json.

| Method | Usage
|:-|-
|POST| To create a new object, your request should specify the POST method.<br/><br/> The POST request includes all of the attributes necessary to create a new object. When you wish to create a new object, send a POST request to the target endpoint.
|GET| For simple retrieval of information about your data, users or application, you should use the GET method. The information you request will be returned to you as a JSON object.<br/><br/> The attributes defined by the JSON object can be used to form additional requests. Any request using the GET method is read-only and will not affect any of the objects you are querying.
|PUT| To update the information about an object in your application, the PUT method is availible.<br/><br/>  Like the DELETE method, the PUT method is idempotent. It sets the state of the target using the provided values, regardless of their current values. Requests using the PUT method do not need to check the current attributes of the object. For every use of the PUT method it's required to include actual version of the object.
|PATCH|To update just some information about an object in your application, the PATCH method is availible.
|DELETE|To destroy an object or delete an user and remove it from your application, the DELETE method should be used. This will remove the specified object if it is found.<br/><br/>  If it is not found, the operation will return a response indicating that the object was not found. This idempotency means that you do not have to check for a resource's availability prior to issuing a delete command, the final state will be the same regardless of its existence.

###HTTP Statuses
Along with the HTTP methods that the API responds to, it will also return standard HTTP statuses, including error codes.

In the event of a problem, the status will contain the error code, while the body of the response will usually contain additional information about the problem that was encountered.

In general, if the status returned is in the 200 range, it indicates that the request was fulfilled successfully and that no error was encountered.

Return codes in the 400 range typically indicate that there was an issue with the request that was sent. Among other things, this could mean that you did not authenticate correctly, that you are requesting an action that you do not have authorization for, that the object you are requesting does not exist, or that your request is malformed.

If you receive a status in the 500 range, this generally indicates a server-side problem. This means that we are having an issue on our end and cannot fulfill your request currently.

**Example error response**
```json
{
    "status": "error",
    "code": "SKIT01-001",
    "message": "This endpoint does not exist."
}
```

###Responses
When a request is successful, a response body will typically be sent back in the form of a JSON object. An exception to this is when a DELETE request is processed, which will result in a successful HTTP 200 status and an empty response body.

The response will be a JSON object for a request on a single object and an array of objects for a request on a collection of objects.

**Example single object response**
```json
{
    "name": "Palpatine",
    "position": "Supreme Chancellor"
}
```

**Example multiple objects response**
```json
[
    {
        "name": "Anakin Skywalker",
        "position": "Jedi Knight"
    },
    {
        "name": "Admiral Motti",
        "position": "Imperial officer"
    }
]
```

###Authorization
SynergyKIT API v2.1 uses basic authorization. Authorization is done via HTTP headers. For example, if the name of your application is Demo, base url is:

`https://demo.api.synergykit.com/v2.1`

**Curl example**
```text
curl -X GET \
-H "Content-Type: application/json" \
-H "Authorization: Basic c3luZXJneWtpdC1zYW1wbGUtYXBwOmEwM2YyZWUxLTU5ZTItNDYzZC1hMzBiLTAyOTIwMDc1ZjUzMA==" \
https://demo.api.synergykit.com/v2.1/
```

**Response body**
```json
{
    "name": "SynergyKit Api",
    "version": "2.1.4",
    "tenant": "demo",
    "key": "03206299-937b-44c3-8416-b310ad32d28b"
}
```

##Documents

Documents are data saved in collections. Collections are basically tables in database where you can store your data. By sending requests to the documents endpoint, you can list, create, update or delete documents.

###Create a new document
To create a new document in collection example, send a **POST** request to

`https://demo.api.synergykit.com/v2.1/data/example`

| Method | Usage | Description
|:-|:-|-
|_id|String|A unique identifier for each document instance. This is automatically generated upon document creation.
|updatedAt| Number  |Timestamp when was document last updated. For the first post is timestamp same as createdAt parameter.
|createdAt| Number  |Timestamp when was document created.
|user_ids| Array of strings| Array of user ids, who have access this document. By default, id of logged user is inserted in. If no user is logged in, `"anonymous"` id is inserted.
|__v|   Number| Actual version of document. It is increased after every update.
| * | ? | Any additional data

**Curl example**

```text
curl -X POST \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
-d '{"name": "Anakin Skywalker", "lightsaber": "blue"}' \
https://demo.api.synergykit.com/v2.1/data/example
```

A document will be created using the provided information. The response body will contain a JSON object.

**Response body**

```json
{
    "__v": 0,
    "createdAt": 1418140838770,
    "user_ids": ["anonymous"],
    "_id": "2393265f-cfee-429a-ad04-3d2fbd1b126d",
    "name": "Anakin Skywalker",
    "lightsaber": "blue",
    "updatedAt": 1418140838770
}
```

### Retrieve an existing document by ID

To show an individual document, send a **GET** request to

`https://demo.api.synergykit.com/v2.1/data/example/2393265f-cfee-429a-ad04-3d2fbd1b126d`

**Curl example**
```text
curl -X GET \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
https://demo.api.synergykit.com/v2.1/data/example/2393265f-cfee-429a-ad04-3d2fbd1b126d
```

The response body will contain a JSON object.

**Response body**
```json
{
    "_id": "2393265f-cfee-429a-ad04-3d2fbd1b126d",
    "user_ids": ["anonymous"],
    "createdAt": 1418140838770,
    "name": "Anakin Skywalker",
    "lightsaber": "blue",
    "updatedAt": 1418140838770,
    "__v": 0
}
```

### Update document
To update document, send a **PUT** request to

`https://demo.api.synergykit.com/v2.1/data/example/2393265f-cfee-429a-ad04-3d2fbd1b126d`

**Curl example**
```text
curl -X PUT \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
-d '{"__v": 0, "name": "Darth Vader", "lightsaber": "red", "darkside": true}' \
https://demo.api.synergykit.com/v2/data/example/2393265f-cfee-429a-ad04-3d2fbd1b126d
```
The response body will contain a JSON object. Notice, that the version was increased by 1.

**Response body**
```json
{
    "_id": "2393265f-cfee-429a-ad04-3d2fbd1b126d",
    "user_ids": ["anonymous"],
    "createdAt": 1418140838770,
    "name": "Darth Vader",
    "lightsaber": "red",
    "updatedAt": 1418142720747,
    "__v": 1,
    "darkside": true
}
```



### Delete document
To delete document, send a **DELETE** request to

`https://demo.api.synergykit.com/v2.1/data/example/2393265f-cfee-429a-ad04-3d2fbd1b126d`

```text
curl -X DELETE \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
https://demo.api.synergykit.com/v2/data/example/2393265f-cfee-429a-ad04-3d2fbd1b126d
```

The response body will contain an empty JSON object.

## Real-time data observerving
SynergyKit data is retrieved by attaching an asynchronous listener to a collection. The listener will be triggered anytime the data changes. This section covers the basics of retrieving data, and how to perform simple queries.

Following examples are written in Node.js using Socket.io

### Connect to api

```javascript
var io = require("socket.io-client");
var socket = io("https://demo.api.synergykit.com", {
    secure: true
});
```

### Start observing whole collection

Listening for new documents created in collection example.

```javascript
socket.on("connect", function() {

    // Subscribe to observing
    socket.emit("subscribe", {
        tenant: "demo",
        key: "LKJELHFhlehwflw797ehf",
        token: "your_session_token",
        eventName: "created",
        collectionName: "example"
    });
    
    // Start observing collection example on event created
    socket.on("created_example", function(data) {
        console.log(data);
    });
});
```

**Availible events**

|Event name|Description|
|:-|-
|`created`| Listen to all new documents in collection
|`updated`| Listen to all updated documents in collection
|`patched`| Listen to all patched documents in collection
|`deleted`| Listen to all deleted documents in collection

### Start observing collection with filter

Listening for new documents created in collection example and passing our filter

```javascript
socket.on("connect", function() {
    
    var filterName = "surname";
    
    // Subscribe to observing with filter
    socket.emit("subscribe", {
        tenant: "demo",
        key: "LKJELHFhlehwflw797ehf",
        token: "your_session_token",
        filter: {
            name: filterName,
            query: "'surname' eq 'Skywalker'"
        },
        eventName: "created",
        collectionName: "example"
    });
    
    // Start observing collection example on event created and filter name
    socket.on("created_example_" + filterName, function(data) {
        console.log(data);
    });
});
```

### Stop observing

Unsubscribe from listening messages about new documents in collection example

```javascript
socket.on("connect", function() {

    // Unsubscribe from observing
    socket.emit("unsubscribe", {
        tenant: "demo",
        key: "LKJELHFhlehwflw797ehf",
        token: "your_session_token",
        eventName: "created",
        collectionName: "example"
    });
});
```

### Speak communication

Speak is useful, when you want send message to another listeners, but don't want to save it in database.

#### Send speak
```javascript
socket.on("connect", function() {

    // Emit speak message
    socket.emit("speak", {
        tenant: "demo",
        token: "your_session_token",
        eventName: "newMessage",
        message: "Hellow Anakin"
    });
});
```

#### Receive speak
```javascript
socket.on("connect", function() {

    // Subscribe for listening
    socket.emit("subscribe", {
        tenant: "demo",
        key: "LKJELHFhlehwflw797ehf",
        token: "your_session_token",
        eventName: "newMessage",
    });
    
    // Start listening event newMessage
    socket.on("newMessage", function(message) {
        console.log(message);
    });
});
```

## Queries
You can retrieve multiple objects at once by sending a **GET** request to the class URL. Without any URL parameters, this simply lists objects in the class.

For more complex filtering and sorting SynergyKIT accepts OData standard. These queries can be used with data, users and files endpoints.

### OData
The OData Protocol specification defines how to standardize a typed, resource-oriented CRUD interface for manipulating data sources by providing collections of entries which must have required elements.

### Filter
Uses key word **$filter**.

A Boolean expression for whether a particular entry should be included in the feed, e.g. /data/example?$filter=lightsaber eq 'blue'. The Query Expression section describes OData expressions.

In filter option you can use these operators.

|Operation|Example|Description|
|:-|:-|-
|And|   x and y|    Conditional and.|
|Or|    x or y| Conditional or.|
|Not|   not x|  Logical not.|
|Less than| x lt y| |
|Greater than|  x gt y| |
|Less than or equal|    x le y| |
|Greater than or equal| x ge y| |
|Equals|    x eq y| |
|Not equals|    x ne y| |
|In array|  x in 'foo,bar'| Searching for value in array of strings.|
|Not in array|  x nin 'foo,bar'|    Searching for value which is not in array of strings.|

In filter option you can use these built-in methods.

|Method|    Example|    Description|
|:-|:-|-
|startswith|    startswith(x,'foo')|    Whether the beginning of the first parameter values matches the second parameter value.
|endswith|  endswith(x,'foo')| Whether the end of the first parameter value matches the second parameter value.
|substringof|   substringof(x,'foo')    | String value starting at the character index specified by the second parameter value in the first parameter string value. Selecting length is specified by the third parameter.

### Select
Uses key word **$select**.

Limit the properties on each entry to just those requested, e.g. /data/example?$select=lightsaber,name.

### Inline count
Uses key word **$inlinecount**.

A Boolean value of true or false request a count of the matching resources included with the resources in the response, e.g. /data/example?$inlinecount=true

### Top
Uses key word **$top**.

Return entries from the top of the feed, e.g. /data/example?$top=4.

### Skip
Uses key word **$skip**.

How many entries you’d like to skip, e.g. /data/example?$skip=4.

### Order by
Uses key word **$orderby**.

One or more comma-separated expressions with an optional “asc” (the default) or “desc” depending on the order you’d like the values sorted, e.g. /data/example?$orderby=createdAt desc.

### Querying
You can use query with **data**, **users** and **files** endpoints

## Users
Users are alfa and omega of every application. In SynergyKit you can easily work with your users by methods listed below. By sending requests to the users endpoint, you can list, create, update or delete users.

### Create a new user
To create a new user, send a **POST** request to

`https://demo.api.synergykit.com/v2.1/users`


**Curl example**
```text
curl -X POST \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
-d '{"name": "Anakin Skywalker", "password":"test", "email": "anakin@tatooine.planet"}' \
https://demo.api.synergykit.com/v2.1/users
```

|Parameter  |Type   |Description| |
|:-|:-|-|:-
|email| String| E-mail address of user. String is unique identificator, if you provide it, you can not have two users with same email address.  | **required**
|password|  String| Password of user.| **required** 
|isActivated|   Boolean|    You can set that your user is already activated. Default value is set to false.|    
|*  |?| You can set any other parameters to your user.|

An user will be created using the provided information. The response body will contain a JSON object.

**Response body**
```json
{
    "__v": 0,
    "email": "anakin@tatooine.planet",
    "name": "Anakin Skywalker",
    "isActivated": false,
    "activationHash": "d09356b4b2056b5bfca6d119c8f988ce53f2335b",
    "platforms": [],
    "roles": [],
    "authData": {},
    "updatedAt": 1421664263534,
    "createdAt": 1421664263688,
    "_id": "429fad57-650a-47bb-ade4-3978c1737fb9"
}
```

|Parameter  |Type   |Description
|:-|:-|-
|_id|   String| A unique identifier for each user instance. This is automatically generated upon user creation.
|email| String| Email which you posted.
|isActivated|   Boolean|    Shows if the user is activated or not.
|activationHash|    String| Automatically generated hash for activation purposes.
|platforms| Array of objects|   Array containing all platforms, for which you registered your user. Each object contain information about application url, name of platform, registration ID and development state.
|roles| Array of strings| Array containing all roles of user
|authData| Object| Contains data about linked user from social networks
|updatedAt| Number| Timestamp when was user last updated. For the first post is timestamp same as createdAt parameter.
|createdAt| Number| Timestamp when was user created.
|__v|   Number| Actual version of user. It is increased after every update.

### Verifying email
By default, user is not activated. This mean, that you can use this state to validate user email address by sending him activation link.

To activate user, send an email with this activation link

`https://demo.api.synergykit.com/v2.1/users/activation/9d555815f0265c2270a7bbf3b1ea3d4e09ac48ae?callback=https://synergykit.com`

You can provide parameter callback with url address where you want to redirect user after activation.

### Login user
After you allow users to sign up, you need to let them log into their account with an email and password in the future. To do this, send a POST request to

`https://demo.api.synergykit.com/v2.1/users/login`

**Curl example**
```text
curl -X POST \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
-d '{"email": "anakin@tatooine.planet", "password":"test"}' \
https://demo.api.synergykit.com/v2.1/users/login
```

If user will be successfully logged in, response body will contain a JSON object with user.

**Response body**
```json
{
    "_id": "2dba8954-0c42-46d0-9dad-90f9236a4774",
    "isActivated": true,
    "sessionToken": "QxNi1iMzEwYWQzMmQyOGzowMzIwN",
    "platforms": [],
    "roles": [],
    "authData": {},
    "updatedAt": 1418145026788,
    "createdAt": 1418143678670,
    "__v": 1,
}
```

### Retrieve an existing user by ID
To show an individual user, send a **GET** request to

`https://demo.api.synergykit.com/v2.1/users/65fcc878-1f87-478f-851e-a0aaedade8b2`

**Curl example**
```text
curl -X GET \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
https://demo.api.synergykit.com/v2.1/users/65fcc878-1f87-478f-851e-a0aaedade8b2
```

The response body will contain a JSON object.

**Response body**
```json
{
    "__v": 0,
    "email": "anakin@tatooine.planet",
    "name": "Anakin Skywalker",
    "isActivated": false,
    "activationHash": "9d555815f0265c2270a7bbf3b1ea3d4e09ac48ae",
    "platforms": [],
    "roles": [],
    "authData": {},
    "updatedAt": 1418144907372,
    "createdAt": 1418144907377,
    "_id": "65fcc878-1f87-478f-851e-a0aaedade8b2"
}
```

### Update user
To update user, send a **PUT** request to

`https://demo.api.synergykit.com/v2.1/users/2dba8954-0c42-46d0-9dad-90f9236a4774`

**Curl example**
```text
curl -X PUT \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
-d '{"name": "Darth Vader", "email": "vader@death.star", "__v": 0}' \
https://demo.api.synergykit.com/v2.1/users/2dba8954-0c42-46d0-9dad-90f9236a4774
```

The response body will contain a JSON object. Please notice, that the version was increased by 1.
**Response body**
```json
{
    "_id": "2dba8954-0c42-46d0-9dad-90f9236a4774",
    "isActivated": false,
    "activationHash": "1361bab136c036a1c7bdf5557d44deae8f51f98c",
    "platforms": [],
    "roles": [],
    "authData": {},
    "updatedAt": 1418145026788,
    "createdAt": 1418143678670,
    "__v": 1,
    "email": "vader@death.star",
    "name": "Darth Vader"
}
```

### Delete user
To delete user, send a **DELETE** request to
`https://demo.api.synergykit.com/v2.1/users/2dba8954-0c42-46d0-9dad-90f9236a4774`

**Curl example**
```text
curl -X DELETE \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
https://demo.api.synergykit.com/v2.1/users/2dba8954-0c42-46d0-9dad-90f9236a4774
```

The response body will contain an empty JSON object.

### Add role
To add role to user, send a **POST** request to
`https://demo.api.synergykit.com/v2.1/users/2dba8954-0c42-46d0-9dad-90f9236a4774/roles`

**Curl example**
```text
curl -X POST \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
-d '{"role": "pilot"}' \
https://demo.api.synergykit.com/v2.1/users/2dba8954-0c42-46d0-9dad-90f9236a4774/roles
```

The response body will contain a JSON object.

**Response body**
```json
{
    "_id": "2dba8954-0c42-46d0-9dad-90f9236a4774",
    "isActivated": false,
    "activationHash": "1361bab136c036a1c7bdf5557d44deae8f51f98c",
    "platforms": [],
    "roles": ["pilot"],
    "authData": {},
    "updatedAt": 1418145026788,
    "createdAt": 1418143678670,
    "__v": 1,
    "email": "vader@death.star",
    "name": "Darth Vader"
}
```

### Remove role
To remove role from user, send a **DELETE** request to
`https://demo.api.synergykit.com/v2.1/users/2dba8954-0c42-46d0-9dad-90f9236a4774/roles/pilot`

**Curl example**
```text
curl -X DELETE \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
https://demo.api.synergykit.com/v2.1/users/2dba8954-0c42-46d0-9dad-90f9236a4774/roles/pilot
```

The response body will contain a JSON object.

**Response body**
```json
{
    "_id": "2dba8954-0c42-46d0-9dad-90f9236a4774",
    "isActivated": false,
    "activationHash": "1361bab136c036a1c7bdf5557d44deae8f51f98c",
    "platforms": [],
    "roles": [],
    "authData": {},
    "updatedAt": 1418145026788,
    "createdAt": 1418143678670,
    "__v": 1,
    "email": "vader@death.star",
    "name": "Darth Vader"
}
```

### Add platform to user
Platforms are useful for pairing individual mobile devices or web applications to the user via registration ID. After assignment platform to the user you will be able to send push notifications to the device or application.

To add platform to user, send a **POST** request to
`https://demo.api.synergykit.com/v2.1/users/65fcc878-1f87-478f-851e-a0aaedade8b2/platforms`

**Curl example**
```text
curl -X POST \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
-d '{"platformName": "android", "registrationId": "1234ABCD5678"}' \
https://demo.api.synergykit.com/v2.1/users/65fcc878-1f87-478f-851e-a0aaedade8b2/platforms
```


|Parameter| Type|   Description | |
|:-|:-|-|:-
|platformName|  String| Name of the platform. Availible platforms are 'android', 'apple' and 'web'.|**required**
|registrationId|    String| Registration ID which can be obtained in the device.| **required**
|development|   Boolean|    You can decide if the platform is used for developing purposes or not.| 

The platform will be added to the user. Response body will contain a JSON object with added platform.

**Response body**
```json
{
    "__v": 0,
    "_id": "2393265f-cfee-429a-ad04-3d2fbd1b126d",
    "development": false,
    "registrationId": "1234ABCD5678",
    "platformName": "android"
}
```
### Retrieve platform 
To show an individual platform user, send a **GET** request to
`https://demo.api.synergykit.com/v2.1/users/65fcc878-1f87-478f-851e-a0aaedade8b2/platforms/2393265f-cfee-429a-ad042fbd1b126d`

**Curl example**
```text
curl -X GET \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
https://demo.api.synergykit.com/v2.1/users/65fcc878-1f87-478f-851e-a0aaedade8b2/platforms/2393265f-cfee-429a-ad04-3d2fbd1b126d
```

The response body will contain a JSON object.

**Response body**
```json
{
    "__v": 0,
    "_id": "2393265f-cfee-429a-ad04-3d2fbd1b126d",
    "development": false,
    "registrationId": "1234ABCD5678",
    "platformName": "android"
}
```

### Update platform
To update platform of user, send a **PUT** request to

`https://demo.api.synergykit.com/v2.1/users/65fcc878-1f87-478f-851e-a0aaedade8b2/platforms/2393265f-cfee-429a-ad042fbd1b126d`

**Curl example**
```text
curl -X PUT \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
-d '{"development": true}' \
https://demo.api.synergykit.com/v2.1/users/65fcc878-1f87-478f-851e-a0aaedade8b2/platforms/2393265f-cfee-429a-ad04-3d2fbd1b126d
```

The response body will contain a JSON object.

**Response body**
```json
{
    "__v": 1,
    "_id": "2393265f-cfee-429a-ad04-3d2fbd1b126d",
    "development": true,
    "registrationId": "1234ABCD5678",
    "platformName": "android"
}
```

### Delete platform
To remove platform of user, send a **DELETE** request to
`https://demo.api.synergykit.com/v2.1/users/65fcc878-1f87-478f-851e-a0aaedade8b2/platforms/2393265f-cfee-429a-ad042fbd1b126d`

**Curl example**
```text
curl -X DELETE \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
https://demo.api.synergykit.com/v2.1/users/65fcc878-1f87-478f-851e-a0aaedade8b2/platforms/2393265f-cfee-429a-ad04-3d2fbd1b126d
```

The response body will contain an empty JSON object.

### Linking users
SynergyKit allows you to link your users with services like Twitter, Facebook and Google+, enabling your users to sign up or log into your application using their existing identities. This is accomplished through the sign-up REST endpoint by providing authentication data for the service you wish to link to a user in the authData field. Once your user is associated with a service, the authData for the service will be stored with the user and is retrievable by logging in.

authData is a JSON object with keys for each linked service containing the data below. In each case, you are responsible for completing the authentication flow (e.g. OAuth 1.0a) to obtain the information the the service requires for linking.

#### Facebook authData
```json
{
    "facebook": {
        "id": "user's Facebook id number as a string",
        "access_token": "an authorized Facebook access token for the user"
    }
}
```

#### Twitter authData
```json
{
    "twitter": {
        "id": "user's Twitter id number as a string",
        "screen_name": "user's Twitter screen name",
        "consumer_key": "your application's consumer key",
        "consumer_secret": "your application's consumer secret",
        "auth_token": "an authorized Twitter token for the user with your application",
        "auth_token_secret": "the secret associated with the auth_token"
    }
}
```

#### Google+ authData
```json
{
    "google": {
        "id": "user's Google+ id number as a string"
    }
}
```

#### Anonymous authData
```json
{
    "anonymous": {}
}
```

#### Signing Up and Logging In
Signing a user up with a linked service and logging them in with that service uses the same **POST** request, in which the authData for the user is specified. For example, to sign up or log in with a user's Facebook account:

`https://demo.api.synergykit.com/v2.1/users`

**Curl Example**

```text
curl -X POST \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
-d '{
    "authData": {
        "facebook": {
                "id": "12345678",
                "access_token": "zIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwY",
            }
        }
    }' \
https://demo.api.synergykit.com/v2.1/users
```

The new user or logged user will be returned.

**Response body**
```json
{
    "_id": "2dba8954-0c42-46d0-9dad-90f9236a4774",
    "isActivated": true,
    "sessionToken": "QxNi1iMzEwYWQzMmQyOGzowMzIwN",
    "platforms": [],
    "roles": [],
    "authData": {
        "facebook": {
            "id": "12345678",
            "access_token": "zIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwY",
        }
    },
    "updatedAt": 1418145026788,
    "createdAt": 1418143678670,
    "__v": 1,
}
```


## Communication
In SynergyKit you can communicate with your users by different ways. There are listed some methods below this section.

One way is sending push notifications into user devices. This action needs to have filled your API key for Android devices in Settings, section Android. For push notifications into iOS devices you need to fill your password and certificates into Apple section in Settings.

Another way is sending emails to your users. For this you need to create email templates in administration under Mailing section.

### Send notification
To send push notification to users, send a **POST** request to

`https://demo.api.synergykit.com/v2.1/users/notification`

**Curl example**
```text
curl -X POST \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
-d '{"userIds": "65fcc878-1f87-478f-851e-a0aaedade8b2", "alert": "Use the force!"}' \
https://demo.api.synergykit.com/v2.1/users/notification
```

|Parameter| Type    |Description| |
|:-|:-|-|:-
|userIds|   String or Array of Strings| IDs of user(s) which you want send push notification. |**required**
|alert| String| Message which will be shown in notification bar.    |
|sound| String| Sound to play on target device. (Works on iOS devices only).    |
|badge| String| The number which will be shown in badge. (Works on iOS devices only).|  
|payload|   String| Additional data. (Works on iOS devices only).|  

The response body will contain an empty JSON object.

### Send e-mail
To send email, you need to specify template first. For this example lets use the prepared template in administration called Example, under section Mailing.

To send email, send **POST** request to 

`https://demo.api.synergykit.com/v2.1/mail/example`

**Curl example**
```text
curl -X POST \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
-d '{"subject": "Hello Anakin", "email": "anakin@tatooine.planet", "name": "Anakin"}' \
https://demo.api.synergykit.com/v2.1/mail/example
```

The response body will contain an empty JSON object.

## Files
SynergyKit can be also used for storing as much quantity of files as you need for your application.

### Upload file
To upload a file to SynergyKit, send a **POST** request to

`https://demo.api.synergykit.com/v2.1/files`

**Curl example**
```text
curl -X POST \
-H "Content-Type: multipart/form-data" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
-F "filedata=@test_image.jpg" \
https://demo.api.synergykit.com/v2.1/files
```

The response body will containt JSON object.

```json
{
    "__v": 0,
    "size": 294119,
    "extension": "jpg",
    "path": "https://synergykit.blob.core.windows.net/demo/ad2806dc5d9f5f86656c43cd95156bcf.jpg",
    "filename": "ad2806dc5d9f5f86656c43cd95156bcf.jpg",
    "applicationUrl": "demo",
    "updatedAt": 1421507284342,
    "createdAt": 1421507284342,
    "_id": "62fc07ea-9123-443c-ac66-c1eaa627a4a9"
}
```

### Retrieve file by ID
To retrieve a file by ID, send a **GET** request to

`https://demo.api.synergykit.com/v2.1/files/62fc07ea-9123-443c-ac66-c1eaa627a4a9`

**Curl example**
```text
curl -X GET \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
https://demo.api.synergykit.com/v2.1/files/62fc07ea-9123-443c-ac66-c1eaa627a4a9
```

The response body will containt JSON object.

```json
{
    "__v": 0,
    "size": 294119,
    "extension": "jpg",
    "path": "https://synergykit.blob.core.windows.net/demo/ad2806dc5d9f5f86656c43cd95156bcf.jpg",
    "filename": "ad2806dc5d9f5f86656c43cd95156bcf.jpg",
    "applicationUrl": "demo",
    "updatedAt": 1421507284342,
    "createdAt": 1421507284342,
    "_id": "62fc07ea-9123-443c-ac66-c1eaa627a4a9"
}
```

### Delete file
To delete file, send a **DELETE** request to

`https://demo.api.synergykit.com/v2.1/files/62fc07ea-9123-443c-ac66-c1eaa627a4a9`

**Curl example**
```text
curl -X DELETE \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
https://demo.api.synergykit.com/v2.1/files/62fc07ea-9123-443c-ac66-c1eaa627a4a9
```

The response body will contain an empty JSON object.

## Cloud Code
Our vision is to let developers build any app without dealing with servers. For complex apps, sometimes you just need a bit of logic that isn't running on a mobile device. Cloud Code makes this possible.

**Cloud Code example**
```javascript
// Create instance of Data object and as first parameter specify the collection where to save
var spaceShip = Synergykit.Data("SpaceShips");

// Set any properities you want
spaceShip.set("type", "Star Fighter");
spaceShip.set("code", "ARC-170");
spaceShip.set("description", "Protecting the skies over Republic worlds were specialized clone fighter forces flying the latest in starfighter technology.");

// And save data to SynergyKit
spaceShip.save({
    success: function(spaceShip, statusCode) {
        callback(spaceShip);
    },
    error: callback
});
```

In Cloud Code there are some prepare functions to work with.

|Function|Description
|:-|-
|`log(message)`|Save message to logs in administration and also in console
|`console.log(message)`|Log message in console
|`callback(result, statusCode)`|Return `result` in response with `statusCode` defined. By default, `result` is `{}` and `statusCode` is `200`
|`require(module)`| Require availible modules listed below

You have also access to request body in variable params or parameters.

### Modules
Cloud Code runs in the Node.js jailed sandbox and uses strict JavaScript language with some prepared modules and variables, which you can use for your development. You have access to Node.js SDK in Cloud Code and modules which can be require.

#### Moment.js

```javascript
var moment = require('moment');
callback(moment);
```

#### Request

```javascript
var request = require('request');
request.get({
    uri: "https://demo.api.synergykit.com/v2.1"
}, function(err, response, result) {
    callback(result)
})

```

#### Underscore.js

```javascript
var _ = require("underscore");
callback(_.isString(params.name));
```

#### Urlify

```javascript
var urlify = require("urlify").create({
    spaces: "-",
    nonPrintable: "-",
    toLower: true,
    trim: true
});
callback(urlify(params.fullname));
```


### Run cloud code
To run cloud code, you need to specify function first. For this example lets use the prepared function in administration called Example, under section Cloud Code.

To run function, send **POST** request to

`https://demo.api.synergykit.com/v2.1/functions/example`

**Curl example**
```text
curl -X POST \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
https://demo.api.synergykit.com/v2.1/functions/example
```
Response will be JSON object sent in callback function.

## Batch request
To reduce the amount of time spent on network round trips, you can get, create, update, or delete up to 50 objects in one call, using the batch endpoint.

### Using batch
Each command in a batch has id, method, endpoint, and body parameters that specify the HTTP command that would normally be used for that command. The commands are run in the order they are given. For example, to create a couple of example objects, send **POST** request to

`https://demo.api.synergykit.com/v2.1/batch`

**Curl example**
```text
curl -X POST \
-H "Content-Type: application/json" \
-H "Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI=" \
-d '[
        {
            "id": 1,
            "method": "POST",
            "endpoint": "/data/example",
            "body": {
                "name": "Anakin Skywalker",
                "lightsaber": "blue"
            }
        },
        {
            "id": 2,
            "method": "POST",
            "endpoint": "/data/example",
            "body": {
                "name": "Darth Vader",
                "lightsaber": "red"
            }
        }
    ]' \
https://demo.api.synergykit.com/v2.1/batch
```

Response will be array of JSON objects.

```json
[{
    "id": 1,
    "statusCode": 200,
    "body": {
        "__v": 0,
        "createdAt": 1430312287559,
        "user_ids": ["anonymous"],
        "_id": "12a09916-16d9-427c-8eff-be0d4b68777e",
        "name": "Anakin Skywalker",
        "lightsaber": "blue",
        "updatedAt": 1430312287559
    }
}, {
    "id": 2,
    "statusCode": 200,
    "body": {
        "__v": 0,
        "createdAt": 1430312288499,
        "user_ids": ["anonymous"],
        "_id": "8cc3079b-40e2-4e1a-95d1-e7b97f216c60",
        "name": "Darth Vader",
        "lightsaber": "red",
        "updatedAt": 1430312288499
    }
}]
```

