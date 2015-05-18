<h2 id="basics">Basics</h2>

<p>Welcome to SynergyKit’s API documentation. We have created a simple name spaced API that allows you full control over your applications.</p>

<p>All of the functionality that you find in our web control panel is available via the API. Today we support all of the major application actions allowing you to build your own control interface using our API.</p>



<h3 id="quick-reference">Quick reference</h3>

<p>All API access is over HTTPS, and accessed via the domain <code>https://tenant.api.synergykit.com</code> The relative path prefix <code>/v2.1</code> indicates that we are currently using version 2.1 of the API.</p>

<table>
<thead>
<tr>
  <th align="left">Endpoint</th>
  <th align="left">HTTP Request</th>
  <th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
  <td align="left"><strong>Documents</strong></td>
  <td align="left"></td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left"><code>/data/&lt;collectionName&gt;</code></td>
  <td align="left">POST</td>
  <td align="left"><a href="#create-a-new-document">Create a new document</a></td>
</tr>
<tr>
  <td align="left"><code>/data/&lt;collectionName&gt;/&lt;documentId&gt;</code></td>
  <td align="left">GET</td>
  <td align="left"><a href="#retrieve-an-existing-document-by-id">Retrieve an existing document by ID</a></td>
</tr>
<tr>
  <td align="left"><code>/data/&lt;collectionName&gt;/&lt;documentId&gt;</code></td>
  <td align="left">PUT</td>
  <td align="left"><a href="#update-document">Update document</a></td>
</tr>
<tr>
  <td align="left"><code>/data/&lt;collectionName&gt;/&lt;documentId&gt;</code></td>
  <td align="left">DELETE</td>
  <td align="left"><a href="#delete-document">Delete document</a></td>
</tr>
<tr>
  <td align="left"><strong>Users</strong></td>
  <td align="left"></td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left"><code>/users</code></td>
  <td align="left">POST</td>
  <td align="left"><a href="#create-a-new-user">Create a new user</a></td>
</tr>
<tr>
  <td align="left"><code>/users/login</code></td>
  <td align="left">POST</td>
  <td align="left"><a href="#login-user">Login user</a></td>
</tr>
<tr>
  <td align="left"><code>/users/&lt;userId&gt;</code></td>
  <td align="left">GET</td>
  <td align="left"><a href="#retrieve-an-existing-user-by-id">Retrieve an existing user by ID</a></td>
</tr>
<tr>
  <td align="left"><code>/users/&lt;userId&gt;</code></td>
  <td align="left">PUT</td>
  <td align="left"><a href="#update-user">Update user</a></td>
</tr>
<tr>
  <td align="left"><code>/users/&lt;userId&gt;</code></td>
  <td align="left">DELETE</td>
  <td align="left"><a href="#delete-user">Delete user</a></td>
</tr>
<tr>
  <td align="left"><code>/users/&lt;userId&gt;/roles</code></td>
  <td align="left">POST</td>
  <td align="left"><a href="#add-role">Add role</a></td>
</tr>
<tr>
  <td align="left"><code>/users/&lt;userId&gt;/roles/&lt;roleUrl&gt;</code></td>
  <td align="left">DELETE</td>
  <td align="left"><a href="#remove-role">Remove role</a></td>
</tr>
<tr>
  <td align="left"><code>/users/me/platforms</code></td>
  <td align="left">POST</td>
  <td align="left"><a href="#add-platform-to-user">Add platform to user</a></td>
</tr>
<tr>
  <td align="left"><code>/users/me/platforms/&lt;platformId&gt;</code></td>
  <td align="left">GET</td>
  <td align="left"><a href="#retrieve-platform">Retrieve platform</a></td>
</tr>
<tr>
  <td align="left"><code>/users/me/platforms/&lt;platformId&gt;</code></td>
  <td align="left">PUT</td>
  <td align="left"><a href="#update-platform">Update platform</a></td>
</tr>
<tr>
  <td align="left"><code>/users/me/platforms/&lt;platformId&gt;</code></td>
  <td align="left">DELETE</td>
  <td align="left"><a href="#delete-platform">Delete platform</a></td>
</tr>
<tr>
  <td align="left"><code>/users</code></td>
  <td align="left">POST</td>
  <td align="left"><a href="#linking-users">Linking users</a></td>
</tr>
<tr>
  <td align="left"><strong>Communication</strong></td>
  <td align="left"></td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left"><code>/users/notification</code></td>
  <td align="left">POST</td>
  <td align="left"><a href="#send-notification">Send notification</a></td>
</tr>
<tr>
  <td align="left"><code>/mail/&lt;templateUrl&gt;</code></td>
  <td align="left">POST</td>
  <td align="left"><a href="#send-e-mail">Send e-mail</a></td>
</tr>
<tr>
  <td align="left"><strong>Files</strong></td>
  <td align="left"></td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left"><code>/files</code></td>
  <td align="left">POST</td>
  <td align="left"><a href="#upload-file">Upload file</a></td>
</tr>
<tr>
  <td align="left"><code>/files/&lt;fileId&gt;</code></td>
  <td align="left">GET</td>
  <td align="left"><a href="#retrieve-file-by-id">Retrieve file by ID</a></td>
</tr>
<tr>
  <td align="left"><code>/files/&lt;fileId&gt;</code></td>
  <td align="left">DELETE</td>
  <td align="left"><a href="#delete-file">Delete file</a></td>
</tr>
<tr>
  <td align="left"><strong>Cloud Code</strong></td>
  <td align="left"></td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left"><code>/functions/&lt;cloudCodeUrl&gt;</code></td>
  <td align="left">POST</td>
  <td align="left"><a href="#run-cloud-code">Run cloud code</a></td>
</tr>
<tr>
  <td align="left"><strong>Batch</strong></td>
  <td align="left"></td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left"><code>/batch</code></td>
  <td align="left">POST</td>
  <td align="left"><a href="#using-batch">Using batch</a></td>
</tr>
</tbody></table>


<h3 id="requests">Requests</h3>

<p>Any tool that is fluent in HTTP can communicate with the API simply by requesting the correct URI. Requests should be made using the HTTPS protocol so that traffic is encrypted. The interface responds to different methods depending on the action required. Whole API is based on CRUD principles.</p>

<p>For POST and PUT requests, the request body must be JSON, with the Content-Type header set to application/json.</p>

<table>
<thead>
<tr>
  <th align="left">Method</th>
  <th>Usage</th>
</tr>
</thead>
<tbody><tr>
  <td align="left">POST</td>
  <td>To create a new object, your request should specify the POST method.<br><br> The POST request includes all of the attributes necessary to create a new object. When you wish to create a new object, send a POST request to the target endpoint.</td>
</tr>
<tr>
  <td align="left">GET</td>
  <td>For simple retrieval of information about your data, users or application, you should use the GET method. The information you request will be returned to you as a JSON object.<br><br> The attributes defined by the JSON object can be used to form additional requests. Any request using the GET method is read-only and will not affect any of the objects you are querying.</td>
</tr>
<tr>
  <td align="left">PUT</td>
  <td>To update the information about an object in your application, the PUT method is availible.<br><br>  Like the DELETE method, the PUT method is idempotent. It sets the state of the target using the provided values, regardless of their current values. Requests using the PUT method do not need to check the current attributes of the object. For every use of the PUT method it’s required to include actual version of the object.</td>
</tr>
<tr>
  <td align="left">PATCH</td>
  <td>To update just some information about an object in your application, the PATCH method is availible.</td>
</tr>
<tr>
  <td align="left">DELETE</td>
  <td>To destroy an object or delete an user and remove it from your application, the DELETE method should be used. This will remove the specified object if it is found.<br><br>  If it is not found, the operation will return a response indicationg that the object was not found. This idempotency means that you do not have eto check for a resource’s availability prior to issuing a delete command, the final state will be the same regardless of its existence.</td>
</tr>
</tbody></table>




<h3 id="http-statuses">HTTP Statuses</h3>

<p>Along with the HTTP methods that the API responds to, it will also return standard HTTP statuses, including error codes.</p>

<p>In the event of a problem, the status will contain the error code, while the body of the response will usually contain additional information about the problem that was encountered.</p>

<p>In general, if the status returned is in the 200 range, it indicates that the request was fulfilled successfully and that no error was encountered.</p>

<p>Return codes in the 400 range typically indicate that there was an issue with the request that was sent. Among other things, this could mean that you did not authenticate correctly, that you are requesting an action that you do not have authorization for, that the object you are requesting does not exist, or that your request is malformed.</p>

<p>If you receive a status in the 500 range, this generally indicates a server-side problem. This means that we are having an issue on our end and cannot fulfill your request currently.</p>

<p><strong>Example error response</strong></p>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">status</span>": <span class="hljs-value"><span class="hljs-string">"error"</span></span>,
    "<span class="hljs-attribute">code</span>": <span class="hljs-value"><span class="hljs-string">"SKIT01-001"</span></span>,
    "<span class="hljs-attribute">message</span>": <span class="hljs-value"><span class="hljs-string">"This endpoint does not exist."</span>
</span>}</code></pre>



<h3 id="responses">Responses</h3>

<p>When a request is successful, a response body will typically be sent back in the form of a JSON object. An exception to this is when a DELETE request is processed, which will result in a successful HTTP 200 status and an empty response body.</p>

<p>The response will be a JSON object for a request on a single object and an array of objects for a request on a collection of objects.</p>

<p><strong>Example single object response</strong></p>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">name</span>": <span class="hljs-value"><span class="hljs-string">"Palpatine"</span></span>,
    "<span class="hljs-attribute">position</span>": <span class="hljs-value"><span class="hljs-string">"Supreme Chancellor"</span>
</span>}</code></pre>

<p><strong>Example multiple objects response</strong></p>



<pre class="prettyprint"><code class="language-json hljs ">[
    {
        "<span class="hljs-attribute">name</span>": <span class="hljs-value"><span class="hljs-string">"Anakin Skywalker"</span></span>,
        "<span class="hljs-attribute">position</span>": <span class="hljs-value"><span class="hljs-string">"Jedi Knight"</span>
    </span>},
    {
        "<span class="hljs-attribute">name</span>": <span class="hljs-value"><span class="hljs-string">"Admiral Motti"</span></span>,
        "<span class="hljs-attribute">position</span>": <span class="hljs-value"><span class="hljs-string">"Imperial officer"</span>
    </span>}
]</code></pre>



<h3 id="authorization">Authorization</h3>

<p>SynergyKIT API v2.1 uses basic authorization. Authorization is done via HTTP headers. For example, if the name of your application is Demo, base url is:</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span></code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs haml">curl -X GET \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic c3luZXJneWtpdC1zYW1wbGUtYXBwOmEwM2YyZWUxLTU5ZTItNDYzZC1hMzBiLTAyOTIwMDc1ZjUzMA=="</span> \
</span>https://demo.api.synergykit.com/v2.1/</code></pre>

<p><strong>Response body</strong></p>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">name</span>": <span class="hljs-value"><span class="hljs-string">"SynergyKit Api"</span></span>,
    "<span class="hljs-attribute">version</span>": <span class="hljs-value"><span class="hljs-string">"2.1.4"</span></span>,
    "<span class="hljs-attribute">tenant</span>": <span class="hljs-value"><span class="hljs-string">"demo"</span></span>,
    "<span class="hljs-attribute">key</span>": <span class="hljs-value"><span class="hljs-string">"03206299-937b-44c3-8416-b310ad32d28b"</span>
</span>}</code></pre>



<h2 id="documents">Documents</h2>

<p>Documents are data saved in collections. Collections are basically tables in database where you can store your data. By sending requests to the documents endpoint, you can list, create, update or delete documents.</p>



<h3 id="create-a-new-document">Create a new document</h3>

<p>To create a new document in collection example, send a <strong>POST</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/data/example</code></pre>

<table>
<thead>
<tr>
  <th align="left">Method</th>
  <th align="left">Usage</th>
  <th>Description</th>
</tr>
</thead>
<tbody><tr>
  <td align="left">_id</td>
  <td align="left">String</td>
  <td>A unique identifier for each document instance. This is automatically generated upon document creation.</td>
</tr>
<tr>
  <td align="left">updatedAt</td>
  <td align="left">Number</td>
  <td>Timestamp when was document last updated. For the first post is timestamp same as createdAt parameter.</td>
</tr>
<tr>
  <td align="left">createdAt</td>
  <td align="left">Number</td>
  <td>Timestamp when was document created.</td>
</tr>
<tr>
  <td align="left">user_ids</td>
  <td align="left">Array of strings</td>
  <td>Array of user ids, who have access this document. By default, id of logged user is inserted in. If no user is logged in, <code>"anonymous"</code> id is inserted.</td>
</tr>
<tr>
  <td align="left">__v</td>
  <td align="left">Number</td>
  <td>Actual version of document. It is increased after every update.</td>
</tr>
<tr>
  <td align="left">*</td>
  <td align="left">?</td>
  <td>Any additional data</td>
</tr>
</tbody></table>


<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs haml">curl -X POST \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>-<span class="ruby">d <span class="hljs-string">'{"name": "Anakin Skywalker", "lightsaber": "blue"}'</span> \
</span>https://demo.api.synergykit.com/v2.1/data/example</code></pre>

<p>A document will be created using the provided information. The response body will contain a JSON object.</p>

<p><strong>Response body</strong></p>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">0</span></span>,
    "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1418140838770</span></span>,
    "<span class="hljs-attribute">user_ids</span>": <span class="hljs-value">[<span class="hljs-string">"anonymous"</span>]</span>,
    "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"2393265f-cfee-429a-ad04-3d2fbd1b126d"</span></span>,
    "<span class="hljs-attribute">name</span>": <span class="hljs-value"><span class="hljs-string">"Anakin Skywalker"</span></span>,
    "<span class="hljs-attribute">lightsaber</span>": <span class="hljs-value"><span class="hljs-string">"blue"</span></span>,
    "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1418140838770</span>
</span>}</code></pre>



<h3 id="retrieve-an-existing-document-by-id">Retrieve an existing document by ID</h3>

<p>To show an individual document, send a <strong>GET</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/data/example/<span class="hljs-number">2393265</span>f-cfee-<span class="hljs-number">429</span>a-ad04-<span class="hljs-number">3</span>d2fbd1b126d</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs haml">curl -X GET \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>https://demo.api.synergykit.com/v2.1/data/example/2393265f-cfee-429a-ad04-3d2fbd1b126d</code></pre>

<p>The response body will contain a JSON object.</p>

<p><strong>Response body</strong></p>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"2393265f-cfee-429a-ad04-3d2fbd1b126d"</span></span>,
    "<span class="hljs-attribute">user_ids</span>": <span class="hljs-value">[<span class="hljs-string">"anonymous"</span>]</span>,
    "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1418140838770</span></span>,
    "<span class="hljs-attribute">name</span>": <span class="hljs-value"><span class="hljs-string">"Anakin Skywalker"</span></span>,
    "<span class="hljs-attribute">lightsaber</span>": <span class="hljs-value"><span class="hljs-string">"blue"</span></span>,
    "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1418140838770</span></span>,
    "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">0</span>
</span>}</code></pre>



<h3 id="update-document">Update document</h3>

<p>To update document, send a <strong>PUT</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/data/example/<span class="hljs-number">2393265</span>f-cfee-<span class="hljs-number">429</span>a-ad04-<span class="hljs-number">3</span>d2fbd1b126d</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs fsharp">curl -X PUT \
-H <span class="hljs-string">"Content-Type: application/json"</span> \
-H <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
-d '{<span class="hljs-string">"__v"</span>: <span class="hljs-number">0</span>, <span class="hljs-string">"name"</span>: <span class="hljs-string">"Darth Vader"</span>, <span class="hljs-string">"lightsaber"</span>: <span class="hljs-string">"red"</span>, <span class="hljs-string">"darkside"</span>: <span class="hljs-keyword">true</span>}' \
https:<span class="hljs-comment">//demo.api.synergykit.com/v2/data/example/2393265f-cfee-429a-ad04-3d2fbd1b126d</span></code></pre>

<p>The response body will contain a JSON object. Notice, that the version was increased by 1.</p>

<p><strong>Response body</strong></p>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"2393265f-cfee-429a-ad04-3d2fbd1b126d"</span></span>,
    "<span class="hljs-attribute">user_ids</span>": <span class="hljs-value">[<span class="hljs-string">"anonymous"</span>]</span>,
    "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1418140838770</span></span>,
    "<span class="hljs-attribute">name</span>": <span class="hljs-value"><span class="hljs-string">"Darth Vader"</span></span>,
    "<span class="hljs-attribute">lightsaber</span>": <span class="hljs-value"><span class="hljs-string">"red"</span></span>,
    "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1418142720747</span></span>,
    "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">1</span></span>,
    "<span class="hljs-attribute">darkside</span>": <span class="hljs-value"><span class="hljs-literal">true</span>
</span>}</code></pre>



<h3 id="delete-document">Delete document</h3>

<p>To delete document, send a <strong>DELETE</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/data/example/<span class="hljs-number">2393265</span>f-cfee-<span class="hljs-number">429</span>a-ad04-<span class="hljs-number">3</span>d2fbd1b126d</code></pre>



<pre class="prettyprint"><code class="language-text hljs haml">curl -X DELETE \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>https://demo.api.synergykit.com/v2/data/example/2393265f-cfee-429a-ad04-3d2fbd1b126d</code></pre>

<p>The response body will contain an empty JSON object.</p>



<h2 id="real-time-data-observerving">Real-time data observerving</h2>

<p>SynergyKit data is retrieved by attaching an asynchronous listener to a collection. The listener will be triggered  anytime the data changes. This section will cover the basics of retrieving data, and how to perform simple queries.</p>

<p>Following examples are written in Node.js using Socket.io</p>



<h3 id="connect-to-api">Connect to api</h3>



<pre class="prettyprint"><code class="language-javascript hljs "><span class="hljs-keyword">var</span> io = <span class="hljs-built_in">require</span>(<span class="hljs-string">"socket.io-client"</span>);
<span class="hljs-keyword">var</span> socket = io(<span class="hljs-string">"https://demo.api.synergykit.com"</span>, {
    secure: <span class="hljs-literal">true</span>
});</code></pre>



<h3 id="start-observing-whole-collection">Start observing whole collection</h3>

<p>Listening for new documents created in collection example.</p>



<pre class="prettyprint"><code class="language-javascript hljs ">socket.on(<span class="hljs-string">"connect"</span>, <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">()</span> {</span>

    <span class="hljs-comment">// Subscribe to observing</span>
    socket.emit(<span class="hljs-string">"subscribe"</span>, {
        tenant: <span class="hljs-string">"demo"</span>,
        key: <span class="hljs-string">"LKJELHFhlehwflw797ehf"</span>,
        token: <span class="hljs-string">"your_session_token"</span>,
        eventName: <span class="hljs-string">"created"</span>,
        collectionName: <span class="hljs-string">"example"</span>
    });

    <span class="hljs-comment">// Start observing collection example on event created</span>
    socket.on(<span class="hljs-string">"created_example"</span>, <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">(data)</span> {</span>
        console.log(data);
    });
});</code></pre>

<p><strong>Availible events</strong></p>

<table>
<thead>
<tr>
  <th align="left">Event name</th>
  <th>Description</th>
</tr>
</thead>
<tbody><tr>
  <td align="left"><code>created</code></td>
  <td>Listen to all new documents in collection</td>
</tr>
<tr>
  <td align="left"><code>updated</code></td>
  <td>Listen to all updated documents in collection</td>
</tr>
<tr>
  <td align="left"><code>patched</code></td>
  <td>Listen to all patched documents in collection</td>
</tr>
<tr>
  <td align="left"><code>deleted</code></td>
  <td>Listen to all deleted documents in collection</td>
</tr>
</tbody></table>




<h3 id="start-observing-collection-with-filter">Start observing collection with filter</h3>

<p>Listening for new documents created in collection example and passing our filter</p>



<pre class="prettyprint"><code class="language-javascript hljs ">socket.on(<span class="hljs-string">"connect"</span>, <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">()</span> {</span>

    <span class="hljs-keyword">var</span> filterName = <span class="hljs-string">"surname"</span>;

    <span class="hljs-comment">// Subscribe to observing with filter</span>
    socket.emit(<span class="hljs-string">"subscribe"</span>, {
        tenant: <span class="hljs-string">"demo"</span>,
        key: <span class="hljs-string">"LKJELHFhlehwflw797ehf"</span>,
        token: <span class="hljs-string">"your_session_token"</span>,
        filter: {
            name: filterName,
            query: <span class="hljs-string">"'surname' eq 'Skywalker'"</span>
        },
        eventName: <span class="hljs-string">"created"</span>,
        collectionName: <span class="hljs-string">"example"</span>
    });

    <span class="hljs-comment">// Start observing collection example on event created and filter name</span>
    socket.on(<span class="hljs-string">"created_example_"</span> + filterName, <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">(data)</span> {</span>
        console.log(data);
    });
});</code></pre>



<h3 id="stop-observing">Stop observing</h3>

<p>Unsubscribe from listening messages about new documents in collection example</p>



<pre class="prettyprint"><code class="language-javascript hljs ">socket.on(<span class="hljs-string">"connect"</span>, <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">()</span> {</span>

    <span class="hljs-comment">// Unsubscribe from observing</span>
    socket.emit(<span class="hljs-string">"unsubscribe"</span>, {
        tenant: <span class="hljs-string">"demo"</span>,
        key: <span class="hljs-string">"LKJELHFhlehwflw797ehf"</span>,
        token: <span class="hljs-string">"your_session_token"</span>,
        eventName: <span class="hljs-string">"created"</span>,
        collectionName: <span class="hljs-string">"example"</span>
    });
});</code></pre>



<h3 id="speak-communication">Speak communication</h3>

<p>Speak is useful, when you want send message to another listeners, but don’t want to save it in database.</p>



<h4 id="send-speak">Send speak</h4>



<pre class="prettyprint"><code class="language-javascript hljs ">socket.on(<span class="hljs-string">"connect"</span>, <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">()</span> {</span>

    <span class="hljs-comment">// Emit speak message</span>
    socket.emit(<span class="hljs-string">"speak"</span>, {
        tenant: <span class="hljs-string">"demo"</span>,
        token: <span class="hljs-string">"your_session_token"</span>,
        eventName: <span class="hljs-string">"newMessage"</span>,
        message: <span class="hljs-string">"Hellow Anakin"</span>
    });
});</code></pre>



<h4 id="receive-speak">Receive speak</h4>



<pre class="prettyprint"><code class="language-javascript hljs ">socket.on(<span class="hljs-string">"connect"</span>, <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">()</span> {</span>

    <span class="hljs-comment">// Subscribe for listening</span>
    socket.emit(<span class="hljs-string">"subscribe"</span>, {
        tenant: <span class="hljs-string">"demo"</span>,
        key: <span class="hljs-string">"LKJELHFhlehwflw797ehf"</span>,
        token: <span class="hljs-string">"your_session_token"</span>,
        eventName: <span class="hljs-string">"newMessage"</span>,
    });

    <span class="hljs-comment">// Start listening event newMessage</span>
    socket.on(<span class="hljs-string">"newMessage"</span>, <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">(message)</span> {</span>
        console.log(message);
    });
});</code></pre>



<h2 id="queries">Queries</h2>

<p>You can retrieve multiple objects at once by sending a <strong>GET</strong> request to the class URL. Without any URL parameters, this simply lists objects in the class.</p>

<p>For more complex filtering and sorting SynergyKIT accepts OData standard. These queries can be used with data, users and files endpoints.</p>



<h3 id="odata">OData</h3>

<p>The OData Protocol specification defines how to standardize a typed, resource-oriented CRUD interface for manipulating data sources by providing collections of entries which must have required elements.</p>



<h3 id="filter">Filter</h3>

<p>Uses key word <strong>$filter</strong>.</p>

<p>A Boolean expression for whether a particular entry should be included in the feed, e.g. /data/example?$filter=lightsaber eq ‘blue’. The Query Expression section describes OData expressions.</p>

<p>In filter option you can use these operators.</p>

<table>
<thead>
<tr>
  <th align="left">Operation</th>
  <th align="left">Example</th>
  <th>Description</th>
</tr>
</thead>
<tbody><tr>
  <td align="left">And</td>
  <td align="left">x and y</td>
  <td>Conditional and.</td>
</tr>
<tr>
  <td align="left">Or</td>
  <td align="left">x or y</td>
  <td>Conditional or.</td>
</tr>
<tr>
  <td align="left">Not</td>
  <td align="left">not x</td>
  <td>Logical not.</td>
</tr>
<tr>
  <td align="left">Less than</td>
  <td align="left">x lt y</td>
  <td></td>
</tr>
<tr>
  <td align="left">Greater than</td>
  <td align="left">x gt y</td>
  <td></td>
</tr>
<tr>
  <td align="left">Less than or equal</td>
  <td align="left">x le y</td>
  <td></td>
</tr>
<tr>
  <td align="left">Greater than or equal</td>
  <td align="left">x ge y</td>
  <td></td>
</tr>
<tr>
  <td align="left">Equals</td>
  <td align="left">x eq y</td>
  <td></td>
</tr>
<tr>
  <td align="left">Not equals</td>
  <td align="left">x ne y</td>
  <td></td>
</tr>
<tr>
  <td align="left">In array</td>
  <td align="left">x in ‘foo,bar’</td>
  <td>Searching for value in array of strings.</td>
</tr>
<tr>
  <td align="left">Not in array</td>
  <td align="left">x nin ‘foo,bar’</td>
  <td>Searching for value which is not in array of strings.</td>
</tr>
</tbody></table>


<p>In filter option you can use these built-in methods.</p>

<table>
<thead>
<tr>
  <th align="left">Method</th>
  <th align="left">Example</th>
  <th>Description</th>
</tr>
</thead>
<tbody><tr>
  <td align="left">startswith</td>
  <td align="left">startswith(x,’foo’)</td>
  <td>Whether the beginning of the first parameter values matches the second parameter value.</td>
</tr>
<tr>
  <td align="left">endswith</td>
  <td align="left">endswith(x,’foo’)</td>
  <td>Whether the end of the first parameter value matches the second parameter value.</td>
</tr>
<tr>
  <td align="left">substringof</td>
  <td align="left">substringof(x,’foo’)</td>
  <td>String value starting at the character index specified by the second parameter value in the first parameter string value. Selecting length is specified by the third parameter.</td>
</tr>
</tbody></table>




<h3 id="select">Select</h3>

<p>Uses key word <strong>$select</strong>.</p>

<p>Limit the properties on each entry to just those requested, e.g. /data/example?$select=lightsaber,name.</p>



<h3 id="inline-count">Inline count</h3>

<p>Uses key word <strong>$inlinecount</strong>.</p>

<p>A Boolean value of true or false request a count of the matching resources included with the resources in the response, e.g. /data/example?$inlinecount=true</p>



<h3 id="top">Top</h3>

<p>Uses key word <strong>$top</strong>.</p>

<p>Return entries from the top of the feed, e.g. /data/example?$top=4.</p>



<h3 id="skip">Skip</h3>

<p>Uses key word <strong>$skip</strong>.</p>

<p>How many entries you’d like to skip, e.g. /data/example?$skip=4.</p>



<h3 id="order-by">Order by</h3>

<p>Uses key word <strong>$orderby</strong>.</p>

<p>One or more comma-separated expressions with an optional “asc” (the default) or “desc” depending on the order you’d like the values sorted, e.g. /data/example?$orderby=createdAt desc.</p>



<h3 id="querying">Querying</h3>

<p>You can use query with <strong>data</strong>, <strong>users</strong> and <strong>files</strong> endpoints</p>



<h2 id="users">Users</h2>

<p>Users are alfa and omega of every application. In SynergyKit you can easily work with your users by methods listed below. By sending requests to the users endpoint, you can list, create, update or delete users.</p>



<h3 id="create-a-new-user">Create a new user</h3>

<p>To create a new user, send a <strong>POST</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/users</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs scilab">curl -X POST \
-H <span class="hljs-string">"Content-Type: application/json"</span> \
-H <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
-d <span class="hljs-string">'{"</span>name<span class="hljs-string">": "</span>Anakin Skywalker<span class="hljs-string">", "</span>password<span class="hljs-string">":"</span>test<span class="hljs-string">", "</span>email<span class="hljs-string">": "</span>anakin@<span class="hljs-transposed_variable">tatooine.</span>planet<span class="hljs-string">"}'</span> \
https:<span class="hljs-comment">//demo.api.synergykit.com/v2.1/users</span></code></pre>

<table>
<thead>
<tr>
  <th align="left">Parameter</th>
  <th align="left">Type</th>
  <th>Description</th>
  <th align="left"></th>
</tr>
</thead>
<tbody><tr>
  <td align="left">email</td>
  <td align="left">String</td>
  <td>E-mail address of user. String is unique identificator, if you provide it, you can not have two users with same email address.</td>
  <td align="left"><strong>required</strong></td>
</tr>
<tr>
  <td align="left">password</td>
  <td align="left">String</td>
  <td>Password of user.</td>
  <td align="left"><strong>required</strong></td>
</tr>
<tr>
  <td align="left">isActivated</td>
  <td align="left">Boolean</td>
  <td>You can set that your user is already activated. Default value is set to false.</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">*</td>
  <td align="left">?</td>
  <td>You can set any other parameters to your user.</td>
  <td align="left"></td>
</tr>
</tbody></table>


<p>An user will be created using the provided information. The response body will contain a JSON object.</p>

<p><strong>Response body</strong></p>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">0</span></span>,
    "<span class="hljs-attribute">email</span>": <span class="hljs-value"><span class="hljs-string">"anakin@tatooine.planet"</span></span>,
    "<span class="hljs-attribute">name</span>": <span class="hljs-value"><span class="hljs-string">"Anakin Skywalker"</span></span>,
    "<span class="hljs-attribute">isActivated</span>": <span class="hljs-value"><span class="hljs-literal">false</span></span>,
    "<span class="hljs-attribute">activationHash</span>": <span class="hljs-value"><span class="hljs-string">"d09356b4b2056b5bfca6d119c8f988ce53f2335b"</span></span>,
    "<span class="hljs-attribute">platforms</span>": <span class="hljs-value">[]</span>,
    "<span class="hljs-attribute">roles</span>": <span class="hljs-value">[]</span>,
    "<span class="hljs-attribute">authData</span>": <span class="hljs-value">{}</span>,
    "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1421664263534</span></span>,
    "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1421664263688</span></span>,
    "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"429fad57-650a-47bb-ade4-3978c1737fb9"</span>
</span>}</code></pre>

<table>
<thead>
<tr>
  <th align="left">Parameter</th>
  <th align="left">Type</th>
  <th>Description</th>
</tr>
</thead>
<tbody><tr>
  <td align="left">_id</td>
  <td align="left">String</td>
  <td>A unique identifier for each user instance. This is automatically generated upon user creation.</td>
</tr>
<tr>
  <td align="left">email</td>
  <td align="left">String</td>
  <td>Email which you posted.</td>
</tr>
<tr>
  <td align="left">isActivated</td>
  <td align="left">Boolean</td>
  <td>Shows if the user is activated or not.</td>
</tr>
<tr>
  <td align="left">activationHash</td>
  <td align="left">String</td>
  <td>Automatically generated hash for activation purposes.</td>
</tr>
<tr>
  <td align="left">platforms</td>
  <td align="left">Array of objects</td>
  <td>Array containing all platforms, for which you registered your user. Each object contain information about application url, name of platform, registration ID and development state.</td>
</tr>
<tr>
  <td align="left">roles</td>
  <td align="left">Array of strings</td>
  <td>Array containing all roles of user</td>
</tr>
<tr>
  <td align="left">authData</td>
  <td align="left">Object</td>
  <td>Contains data about linked user from social networks</td>
</tr>
<tr>
  <td align="left">updatedAt</td>
  <td align="left">Number</td>
  <td>Timestamp when was user last updated. For the first post is timestamp same as createdAt parameter.</td>
</tr>
<tr>
  <td align="left">createdAt</td>
  <td align="left">Number</td>
  <td>Timestamp when was user created.</td>
</tr>
<tr>
  <td align="left">__v</td>
  <td align="left">Number</td>
  <td>Actual version of user. It is increased after every update.</td>
</tr>
</tbody></table>




<h3 id="verifying-email">Verifying email</h3>

<p>By default, user is not activated. This mean, that you can use this state to validate user email address by sending him activation link.</p>

<p>To activate user, send an email with this activation link</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2
<span class="hljs-number">.1</span>/users/activation/<span class="hljs-number">9</span>d555815f0265c2270a7bbf3b1ea3d4e09ac48ae?callback=https://synergykit<span class="hljs-preprocessor">.com</span></code></pre>

<p>You can provide parameter callback with url address where you want to redirect user after activation.</p>



<h3 id="login-user">Login user</h3>

<p>After you allow users to sign up, you need to let them log in to their account with an email and password in the future. To do this, send a POST request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/users/login</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs haml">curl -X POST \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>-<span class="ruby">d <span class="hljs-string">'{"email": "anakin@tatooine.planet", "password":"test"}'</span> \
</span>https://demo.api.synergykit.com/v2.1/users/login</code></pre>

<p>If user will be successfully logged in, response body will contain a JSON object with user.</p>

<p><strong>Response body</strong></p>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"2dba8954-0c42-46d0-9dad-90f9236a4774"</span></span>,
    "<span class="hljs-attribute">isActivated</span>": <span class="hljs-value"><span class="hljs-literal">true</span></span>,
    "<span class="hljs-attribute">sessionToken</span>": <span class="hljs-value"><span class="hljs-string">"QxNi1iMzEwYWQzMmQyOGzowMzIwN"</span></span>,
    "<span class="hljs-attribute">platforms</span>": <span class="hljs-value">[]</span>,
    "<span class="hljs-attribute">roles</span>": <span class="hljs-value">[]</span>,
    "<span class="hljs-attribute">authData</span>": <span class="hljs-value">{}</span>,
    "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1418145026788</span></span>,
    "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1418143678670</span></span>,
    "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">1</span></span>,
}</code></pre>



<h3 id="retrieve-an-existing-user-by-id">Retrieve an existing user by ID</h3>

<p>To show an individual user, send a <strong>GET</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/users/<span class="hljs-number">65</span>fcc878-<span class="hljs-number">1</span>f87-<span class="hljs-number">478</span>f-<span class="hljs-number">851</span>e-a0aaedade8b2</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs haml">curl -X GET \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>https://demo.api.synergykit.com/v2.1/users/65fcc878-1f87-478f-851e-a0aaedade8b2</code></pre>

<p>The response body will contain a JSON object.</p>

<p><strong>Response body</strong></p>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">0</span></span>,
    "<span class="hljs-attribute">email</span>": <span class="hljs-value"><span class="hljs-string">"anakin@tatooine.planet"</span></span>,
    "<span class="hljs-attribute">name</span>": <span class="hljs-value"><span class="hljs-string">"Anakin Skywalker"</span></span>,
    "<span class="hljs-attribute">isActivated</span>": <span class="hljs-value"><span class="hljs-literal">false</span></span>,
    "<span class="hljs-attribute">activationHash</span>": <span class="hljs-value"><span class="hljs-string">"9d555815f0265c2270a7bbf3b1ea3d4e09ac48ae"</span></span>,
    "<span class="hljs-attribute">platforms</span>": <span class="hljs-value">[]</span>,
    "<span class="hljs-attribute">roles</span>": <span class="hljs-value">[]</span>,
    "<span class="hljs-attribute">authData</span>": <span class="hljs-value">{}</span>,
    "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1418144907372</span></span>,
    "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1418144907377</span></span>,
    "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"65fcc878-1f87-478f-851e-a0aaedade8b2"</span>
</span>}</code></pre>



<h3 id="update-user">Update user</h3>

<p>To update user, send a <strong>PUT</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/users/<span class="hljs-number">2</span>dba8954-<span class="hljs-number">0</span>c42-<span class="hljs-number">46</span>d0-<span class="hljs-number">9</span>dad-<span class="hljs-number">90</span>f9236a4774</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs haml">curl -X PUT \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>-<span class="ruby">d <span class="hljs-string">'{"name": "Darth Vader", "email": "vader@death.star", "__v": 0}'</span> \
</span>https://demo.api.synergykit.com/v2.1/users/2dba8954-0c42-46d0-9dad-90f9236a4774</code></pre>

<p>The response body will contain a JSON object. Please notice, that the version was increased by 1. <br>
<strong>Response body</strong></p>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"2dba8954-0c42-46d0-9dad-90f9236a4774"</span></span>,
    "<span class="hljs-attribute">isActivated</span>": <span class="hljs-value"><span class="hljs-literal">false</span></span>,
    "<span class="hljs-attribute">activationHash</span>": <span class="hljs-value"><span class="hljs-string">"1361bab136c036a1c7bdf5557d44deae8f51f98c"</span></span>,
    "<span class="hljs-attribute">platforms</span>": <span class="hljs-value">[]</span>,
    "<span class="hljs-attribute">roles</span>": <span class="hljs-value">[]</span>,
    "<span class="hljs-attribute">authData</span>": <span class="hljs-value">{}</span>,
    "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1418145026788</span></span>,
    "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1418143678670</span></span>,
    "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">1</span></span>,
    "<span class="hljs-attribute">email</span>": <span class="hljs-value"><span class="hljs-string">"vader@death.star"</span></span>,
    "<span class="hljs-attribute">name</span>": <span class="hljs-value"><span class="hljs-string">"Darth Vader"</span>
</span>}</code></pre>



<h3 id="delete-user">Delete user</h3>

<p>To delete user, send a <strong>DELETE</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/users/<span class="hljs-number">2</span>dba8954-<span class="hljs-number">0</span>c42-<span class="hljs-number">46</span>d0-<span class="hljs-number">9</span>dad-<span class="hljs-number">90</span>f9236a4774</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs haml">curl -X DELETE \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>https://demo.api.synergykit.com/v2.1/users/2dba8954-0c42-46d0-9dad-90f9236a4774</code></pre>

<p>The response body will contain an empty JSON object.</p>



<h3 id="add-role">Add role</h3>

<p>To add role to user, send a <strong>POST</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/users/<span class="hljs-number">2</span>dba8954-<span class="hljs-number">0</span>c42-<span class="hljs-number">46</span>d0-<span class="hljs-number">9</span>dad-<span class="hljs-number">90</span>f9236a4774/roles</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs haml">curl -X POST \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>-<span class="ruby">d <span class="hljs-string">'{"role": "pilot"}'</span> \
</span>https://demo.api.synergykit.com/v2.1/users/2dba8954-0c42-46d0-9dad-90f9236a4774/roles</code></pre>

<p>The response body will contain a JSON object.</p>

<p><strong>Response body</strong></p>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"2dba8954-0c42-46d0-9dad-90f9236a4774"</span></span>,
    "<span class="hljs-attribute">isActivated</span>": <span class="hljs-value"><span class="hljs-literal">false</span></span>,
    "<span class="hljs-attribute">activationHash</span>": <span class="hljs-value"><span class="hljs-string">"1361bab136c036a1c7bdf5557d44deae8f51f98c"</span></span>,
    "<span class="hljs-attribute">platforms</span>": <span class="hljs-value">[]</span>,
    "<span class="hljs-attribute">roles</span>": <span class="hljs-value">[<span class="hljs-string">"pilot"</span>]</span>,
    "<span class="hljs-attribute">authData</span>": <span class="hljs-value">{}</span>,
    "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1418145026788</span></span>,
    "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1418143678670</span></span>,
    "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">1</span></span>,
    "<span class="hljs-attribute">email</span>": <span class="hljs-value"><span class="hljs-string">"vader@death.star"</span></span>,
    "<span class="hljs-attribute">name</span>": <span class="hljs-value"><span class="hljs-string">"Darth Vader"</span>
</span>}</code></pre>



<h3 id="remove-role">Remove role</h3>

<p>To remove role from user, send a <strong>DELETE</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/users/<span class="hljs-number">2</span>dba8954-<span class="hljs-number">0</span>c42-<span class="hljs-number">46</span>d0-<span class="hljs-number">9</span>dad-<span class="hljs-number">90</span>f9236a4774/roles/pilot</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs haml">curl -X DELETE \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>https://demo.api.synergykit.com/v2.1/users/2dba8954-0c42-46d0-9dad-90f9236a4774/roles/pilot</code></pre>

<p>The response body will contain a JSON object.</p>

<p><strong>Response body</strong></p>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"2dba8954-0c42-46d0-9dad-90f9236a4774"</span></span>,
    "<span class="hljs-attribute">isActivated</span>": <span class="hljs-value"><span class="hljs-literal">false</span></span>,
    "<span class="hljs-attribute">activationHash</span>": <span class="hljs-value"><span class="hljs-string">"1361bab136c036a1c7bdf5557d44deae8f51f98c"</span></span>,
    "<span class="hljs-attribute">platforms</span>": <span class="hljs-value">[]</span>,
    "<span class="hljs-attribute">roles</span>": <span class="hljs-value">[]</span>,
    "<span class="hljs-attribute">authData</span>": <span class="hljs-value">{}</span>,
    "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1418145026788</span></span>,
    "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1418143678670</span></span>,
    "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">1</span></span>,
    "<span class="hljs-attribute">email</span>": <span class="hljs-value"><span class="hljs-string">"vader@death.star"</span></span>,
    "<span class="hljs-attribute">name</span>": <span class="hljs-value"><span class="hljs-string">"Darth Vader"</span>
</span>}</code></pre>



<h3 id="add-platform-to-user">Add platform to user</h3>

<p>Platforms are useful for pairing individual mobile devices or web applications to the user via registration ID. After assignment platform to the user you will be able to send push notifications to the device or application.</p>

<p>To add platform to user, send a <strong>POST</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/users/me/platforms</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs haml">curl -X POST \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>-<span class="ruby">d <span class="hljs-string">'{"platformName": "android", "registrationId": "1234ABCD5678"}'</span> \
</span>https://demo.api.synergykit.com/v2.1/users/me/platforms</code></pre>

<table>
<thead>
<tr>
  <th align="left">Parameter</th>
  <th align="left">Type</th>
  <th>Description</th>
  <th align="left"></th>
</tr>
</thead>
<tbody><tr>
  <td align="left">platformName</td>
  <td align="left">String</td>
  <td>Name of the platform. Availible platforms are ‘android’, ‘apple’ and ‘web’.</td>
  <td align="left"><strong>required</strong></td>
</tr>
<tr>
  <td align="left">registrationId</td>
  <td align="left">String</td>
  <td>Registration ID which can be obtained in the device.</td>
  <td align="left"><strong>required</strong></td>
</tr>
<tr>
  <td align="left">development</td>
  <td align="left">Boolean</td>
  <td>You can decide if the platform is used for developing purposes or not.</td>
  <td align="left"></td>
</tr>
</tbody></table>


<p>The platform will be added to the user. Response body will contain a JSON object with added platform.</p>

<p><strong>Response body</strong></p>

<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">0</span></span>,
    "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"2393265f-cfee-429a-ad04-3d2fbd1b126d"</span></span>,
    "<span class="hljs-attribute">development</span>": <span class="hljs-value"><span class="hljs-literal">false</span></span>,
    "<span class="hljs-attribute">registrationId</span>": <span class="hljs-value"><span class="hljs-string">"1234ABCD5678"</span></span>,
    "<span class="hljs-attribute">platformName</span>": <span class="hljs-value"><span class="hljs-string">"android"</span>
</span>}</code></pre>



<h3 id="retrieve-platform">Retrieve platform</h3>

<p>To show an individual platform user, send a <strong>GET</strong> request to</p>

<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/users/me/platforms/<span class="hljs-number">2393265</span>f-cfee-<span class="hljs-number">429</span>a-ad042fbd1b126d</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs haml">curl -X GET \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>https://demo.api.synergykit.com/v2.1/users/me/platforms/2393265f-cfee-429a-ad04-3d2fbd1b126d</code></pre>

<p>The response body will contain a JSON object.</p>

<p><strong>Response body</strong></p>

<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">0</span></span>,
    "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"2393265f-cfee-429a-ad04-3d2fbd1b126d"</span></span>,
    "<span class="hljs-attribute">development</span>": <span class="hljs-value"><span class="hljs-literal">false</span></span>,
    "<span class="hljs-attribute">registrationId</span>": <span class="hljs-value"><span class="hljs-string">"1234ABCD5678"</span></span>,
    "<span class="hljs-attribute">platformName</span>": <span class="hljs-value"><span class="hljs-string">"android"</span>
</span>}</code></pre>



<h3 id="update-platform">Update platform</h3>

<p>To update platform of user, send a <strong>PUT</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/users/me/platforms/<span class="hljs-number">2393265</span>f-cfee-<span class="hljs-number">429</span>a-ad042fbd1b126d</code></pre>

<p><strong>Curl example</strong></p>

<pre class="prettyprint"><code class="language-text hljs haml">curl -X PUT \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>-<span class="ruby">d <span class="hljs-string">'{"development": true}'</span> \
</span>https://demo.api.synergykit.com/v2.1/users/me/platforms/2393265f-cfee-429a-ad04-3d2fbd1b126d</code></pre>

<p>The response body will contain a JSON object.</p>

<p><strong>Response body</strong></p>

<h3 id="delete-platform">Delete platform</h3>

<p>To remove platform of user, send a <strong>DELETE</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs lasso">https:<span class="hljs-comment">//demo.api.synergykit.com/v2.1/users/65fcc878-1f87-478f-851e-a0aaedade8b2/platforms/2393265f-cfee-429a</span>
<span class="hljs-string">``</span><span class="hljs-attribute">-ad042fbd1b126d</span><span class="hljs-string">`

**Curl example**
`</span><span class="hljs-string">``</span>text
curl <span class="hljs-attribute">-X</span> DELETE <span class="hljs-subst">\</span>
<span class="hljs-attribute">-H</span> <span class="hljs-string">"Content-Type: application/json"</span> <span class="hljs-subst">\</span>
<span class="hljs-attribute">-H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> <span class="hljs-subst">\</span>
https:<span class="hljs-comment">//demo.api.synergykit.com/v2.1/users/65fcc878-1f87-478f-851e-a0aaedade8b2/platforms/2393265f-cfee-429a-ad04-3d2fbd1b126d</span>




<span class="hljs-subst">&lt;</span>div class<span class="hljs-subst">=</span><span class="hljs-string">"se-preview-section-delimiter"</span><span class="hljs-subst">&gt;&lt;</span>/div<span class="hljs-subst">&gt;</span>
</code></pre>

<p>The response body will contain an empty JSON object.</p>

<h3 id="linking-users">Linking users</h3>

<p>SynergyKit allows you to link your users with services like Twitter, Facebook and Google+, enabling your users to sign up or log into your application using their existing identities. This is accomplished through the sign-up REST endpoint by providing authentication data for the service you wish to link to a user in the authData field. Once your user is associated with a service, the authData for the service will be stored with the user and is retrievable by logging in.</p>

<p>authData is a JSON object with keys for each linked service containing the data below. In each case, you are responsible for completing the authentication flow (e.g. OAuth 1.0a) to obtain the information the the service requires for linking.</p>

<h4 id="facebook-authdata">Facebook authData</h4>

<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">facebook</span>": <span class="hljs-value">{
        "<span class="hljs-attribute">id</span>": <span class="hljs-value"><span class="hljs-string">"user's Facebook id number as a string"</span></span>,
        "<span class="hljs-attribute">access_token</span>": <span class="hljs-value"><span class="hljs-string">"an authorized Facebook access token for the user"</span>
    </span>}
</span>}




&lt;div class=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/div&gt;
</code></pre>

<h4 id="twitter-authdata">Twitter authData</h4>

<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">twitter</span>": <span class="hljs-value">{
        "<span class="hljs-attribute">id</span>": <span class="hljs-value"><span class="hljs-string">"user's Twitter id number as a string"</span></span>,
        "<span class="hljs-attribute">screen_name</span>": <span class="hljs-value"><span class="hljs-string">"user's Twitter screen name"</span></span>,
        "<span class="hljs-attribute">consumer_key</span>": <span class="hljs-value"><span class="hljs-string">"your application's consumer key"</span></span>,
        "<span class="hljs-attribute">consumer_secret</span>": <span class="hljs-value"><span class="hljs-string">"your application's consumer secret"</span></span>,
        "<span class="hljs-attribute">auth_token</span>": <span class="hljs-value"><span class="hljs-string">"an authorized Twitter token for the user with your application"</span></span>,
        "<span class="hljs-attribute">auth_token_secret</span>": <span class="hljs-value"><span class="hljs-string">"the secret associated with the auth_token"</span>
    </span>}
</span>}




&lt;div class=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/div&gt;
</code></pre>

<h4 id="google-authdata">Google+ authData</h4>

<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">google</span>": <span class="hljs-value">{
        "<span class="hljs-attribute">id</span>": <span class="hljs-value"><span class="hljs-string">"user's Google+ id number as a string"</span>
    </span>}
</span>}




&lt;div class=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/div&gt;
</code></pre>

<h4 id="anonymous-authdata">Anonymous authData</h4>

<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">anonymous</span>": <span class="hljs-value">{}
</span>}




&lt;div class=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/div&gt;
</code></pre>

<h4 id="signing-up-and-logging-in">Signing Up and Logging In</h4>

<p>Signing a user up with a linked service and logging them in with that service uses the same <strong>POST</strong> request, in which the authData for the user is specified. For example, to sign up or log in with a user’s Facebook account:</p>

<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/users




&lt;div class=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/div&gt;
</code></pre>

<p><strong>Curl Example</strong></p>

<pre class="prettyprint"><code class="language-text hljs fsharp">curl -X POST \
-H <span class="hljs-string">"Content-Type: application/json"</span> \
-H <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
-d '{
    <span class="hljs-string">"authData"</span>: {
        <span class="hljs-string">"facebook"</span>: {
                <span class="hljs-string">"id"</span>: <span class="hljs-string">"12345678"</span>,
                <span class="hljs-string">"access_token"</span>: <span class="hljs-string">"zIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwY"</span>,
            }
        }
    }' \
https:<span class="hljs-comment">//demo.api.synergykit.com/v2.1/users</span>




&lt;div <span class="hljs-keyword">class</span>=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/div&gt;
</code></pre>

<p>The new user or logged user will be returned.</p>

<p><strong>Response body</strong></p>

<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"2dba8954-0c42-46d0-9dad-90f9236a4774"</span></span>,
    "<span class="hljs-attribute">isActivated</span>": <span class="hljs-value"><span class="hljs-literal">true</span></span>,
    "<span class="hljs-attribute">sessionToken</span>": <span class="hljs-value"><span class="hljs-string">"QxNi1iMzEwYWQzMmQyOGzowMzIwN"</span></span>,
    "<span class="hljs-attribute">platforms</span>": <span class="hljs-value">[]</span>,
    "<span class="hljs-attribute">roles</span>": <span class="hljs-value">[]</span>,
    "<span class="hljs-attribute">authData</span>": <span class="hljs-value">{
        "<span class="hljs-attribute">facebook</span>": <span class="hljs-value">{
            "<span class="hljs-attribute">id</span>": <span class="hljs-value"><span class="hljs-string">"12345678"</span></span>,
            "<span class="hljs-attribute">access_token</span>": <span class="hljs-value"><span class="hljs-string">"zIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwY"</span></span>,
        }
    </span>}</span>,
    "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1418145026788</span></span>,
    "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1418143678670</span></span>,
    "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">1</span></span>,
}




&lt;div class=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/div&gt;
</code></pre>

<h2 id="communication">Communication</h2>

<p>In SynergyKit you can communicate with your users by different ways. There are listed some methods below this section.</p>

<p>One way is to sending push notifications into user devices. This action need to have filled your API key for Android devices in Settings, section Android. For push notifications into iOS devices you need to fill your password and certificates into Apple section in Settings.</p>

<p>Another way is to sending emails to your users. For this you need to create email templates in administration under Mailing section.</p>

<h3 id="send-notification">Send notification</h3>

<p>To send push notification to users, send a <strong>POST</strong> request to</p>

<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/users/notification




&lt;div class=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/div&gt;
</code></pre>

<p><strong>Curl example</strong></p>

<pre class="prettyprint"><code class="language-text hljs haml">curl -X POST \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>-<span class="ruby">d <span class="hljs-string">'{"userIds": "65fcc878-1f87-478f-851e-a0aaedade8b2", "alert": "Use the force!"}'</span> \
</span>https://demo.api.synergykit.com/v2.1/users/notification




&lt;div class="se-preview-section-delimiter"&gt;&lt;/div&gt;
</code></pre>

<table>
<thead>
<tr>
  <th align="left">Parameter</th>
  <th align="left">Type</th>
  <th>Description</th>
  <th align="left"></th>
</tr>
</thead>
<tbody><tr>
  <td align="left">userIds</td>
  <td align="left">String or Array of Strings</td>
  <td>IDs of user(s) which you want send push notification.</td>
  <td align="left"><strong>required</strong></td>
</tr>
<tr>
  <td align="left">alert</td>
  <td align="left">String</td>
  <td>Message which will be shown in notification bar.</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">sound</td>
  <td align="left">String</td>
  <td>Sound to play on target device. (Works on iOS devices only).</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">badge</td>
  <td align="left">String</td>
  <td>The number which will be shown in badge. (Works on iOS devices only).</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">payload</td>
  <td align="left">String</td>
  <td>Additional data. (Works on iOS devices only).</td>
  <td align="left"></td>
</tr>
</tbody></table>


<p>The response body will contain an empty JSON object.</p>

<h3 id="send-e-mail">Send e-mail</h3>

<p>To send email, you need to specify template first. For this example lets use the prepared template in administration called Example, under section Mailing.</p>

<p>To send email, send <strong>POST</strong> request to </p>

<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/mail/example




&lt;div class=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/div&gt;
</code></pre>

<p><strong>Curl example</strong></p>

<pre class="prettyprint"><code class="language-text hljs fsharp">curl -X POST \
-H <span class="hljs-string">"Content-Type: application/json"</span> \
-H <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
-d '{<span class="hljs-string">"subject"</span>: <span class="hljs-string">"Hello Anakin"</span>, <span class="hljs-string">"email"</span>: <span class="hljs-string">"anakin@tatooine.planet"</span>, <span class="hljs-string">"name"</span>: <span class="hljs-string">"Anakin"</span>}' \
https:<span class="hljs-comment">//demo.api.synergykit.com/v2.1/mail/example</span>




&lt;div <span class="hljs-keyword">class</span>=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/div&gt;
</code></pre>

<p>The response body will contain an empty JSON object.</p>

<h2 id="files">Files</h2>

<p>SynergyKit can be also used for storing as much quantity of files as you need for your application.</p>

<h3 id="upload-file">Upload file</h3>

<p>To upload a file to SynergyKit, send a <strong>POST</strong> request to</p>

<pre class="prettyprint"><code class="language-url hljs livecodeserver"><span class="hljs-keyword">https</span>://demo.api.synergykit.com/v2<span class="hljs-number">.1</span>/<span class="hljs-built_in">files</span>




&lt;<span class="hljs-operator">div</span> class=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/<span class="hljs-operator">div</span>&gt;
</code></pre>

<p><strong>Curl example</strong></p>

<pre class="prettyprint"><code class="language-text hljs haml">curl -X POST \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: multipart/form-data"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>-<span class="ruby"><span class="hljs-constant">F</span> <span class="hljs-string">"filedata=@test_image.jpg"</span> \
</span>https://demo.api.synergykit.com/v2.1/files




&lt;div class="se-preview-section-delimiter"&gt;&lt;/div&gt;
</code></pre>

<p>The response body will containt JSON object.</p>

<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">0</span></span>,
    "<span class="hljs-attribute">size</span>": <span class="hljs-value"><span class="hljs-number">294119</span></span>,
    "<span class="hljs-attribute">extension</span>": <span class="hljs-value"><span class="hljs-string">"jpg"</span></span>,
    "<span class="hljs-attribute">path</span>": <span class="hljs-value"><span class="hljs-string">"https://synergykit.blob.core.windows.net/demo/ad2806dc5d9f5f86656c43cd95156bcf.jpg"</span></span>,
    "<span class="hljs-attribute">filename</span>": <span class="hljs-value"><span class="hljs-string">"ad2806dc5d9f5f86656c43cd95156bcf.jpg"</span></span>,
    "<span class="hljs-attribute">applicationUrl</span>": <span class="hljs-value"><span class="hljs-string">"demo"</span></span>,
    "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1421507284342</span></span>,
    "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1421507284342</span></span>,
    "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"62fc07ea-9123-443c-ac66-c1eaa627a4a9"</span>
</span>}




&lt;div class=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/div&gt;
</code></pre>

<h3 id="retrieve-file-by-id">Retrieve file by ID</h3>

<p>To retrieve a file by ID, send a <strong>GET</strong> request to</p>

<pre class="prettyprint"><code class="language-url hljs livecodeserver"><span class="hljs-keyword">https</span>://demo.api.synergykit.com/v2<span class="hljs-number">.1</span>/<span class="hljs-built_in">files</span>/<span class="hljs-number">62</span>fc07ea-<span class="hljs-number">9123</span>-<span class="hljs-number">443</span>c-ac66-c1eaa627a4a9




&lt;<span class="hljs-operator">div</span> class=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/<span class="hljs-operator">div</span>&gt;
</code></pre>

<p><strong>Curl example</strong></p>

<pre class="prettyprint"><code class="language-text hljs livecodeserver">curl -X GET \
-H <span class="hljs-string">"Content-Type: application/json"</span> \
-H <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
<span class="hljs-keyword">https</span>://demo.api.synergykit.com/v2<span class="hljs-number">.1</span>/<span class="hljs-built_in">files</span>/<span class="hljs-number">62</span>fc07ea-<span class="hljs-number">9123</span>-<span class="hljs-number">443</span>c-ac66-c1eaa627a4a9




&lt;<span class="hljs-operator">div</span> class=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/<span class="hljs-operator">div</span>&gt;
</code></pre>

<p>The response body will containt JSON object.</p>

<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">0</span></span>,
    "<span class="hljs-attribute">size</span>": <span class="hljs-value"><span class="hljs-number">294119</span></span>,
    "<span class="hljs-attribute">extension</span>": <span class="hljs-value"><span class="hljs-string">"jpg"</span></span>,
    "<span class="hljs-attribute">path</span>": <span class="hljs-value"><span class="hljs-string">"https://synergykit.blob.core.windows.net/demo/ad2806dc5d9f5f86656c43cd95156bcf.jpg"</span></span>,
    "<span class="hljs-attribute">filename</span>": <span class="hljs-value"><span class="hljs-string">"ad2806dc5d9f5f86656c43cd95156bcf.jpg"</span></span>,
    "<span class="hljs-attribute">applicationUrl</span>": <span class="hljs-value"><span class="hljs-string">"demo"</span></span>,
    "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1421507284342</span></span>,
    "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1421507284342</span></span>,
    "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"62fc07ea-9123-443c-ac66-c1eaa627a4a9"</span>
</span>}




&lt;div class=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/div&gt;
</code></pre>

<h3 id="delete-file">Delete file</h3>

<p>To delete file, send a <strong>DELETE</strong> request to</p>

<pre class="prettyprint"><code class="language-url hljs livecodeserver"><span class="hljs-keyword">https</span>://demo.api.synergykit.com/v2<span class="hljs-number">.1</span>/<span class="hljs-built_in">files</span>/<span class="hljs-number">62</span>fc07ea-<span class="hljs-number">9123</span>-<span class="hljs-number">443</span>c-ac66-c1eaa627a4a9




&lt;<span class="hljs-operator">div</span> class=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/<span class="hljs-operator">div</span>&gt;
</code></pre>

<p><strong>Curl example</strong></p>

<pre class="prettyprint"><code class="language-text hljs livecodeserver">curl -X DELETE \
-H <span class="hljs-string">"Content-Type: application/json"</span> \
-H <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
<span class="hljs-keyword">https</span>://demo.api.synergykit.com/v2<span class="hljs-number">.1</span>/<span class="hljs-built_in">files</span>/<span class="hljs-number">62</span>fc07ea-<span class="hljs-number">9123</span>-<span class="hljs-number">443</span>c-ac66-c1eaa627a4a9




&lt;<span class="hljs-operator">div</span> class=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/<span class="hljs-operator">div</span>&gt;
</code></pre>

<p>The response body will contain an empty JSON object.</p>

<h2 id="cloud-code">Cloud Code</h2>

<p>Our vision is to let developers build any app without dealing with servers. For complex apps, sometimes you just need a bit of logic that isn’t running on a mobile device. Cloud Code makes this possible.</p>

<p><strong>Cloud Code example</strong></p>

<pre class="prettyprint"><code class="language-javascript hljs "><span class="hljs-comment">// Create instance of Data object and as first parameter specify the collection where to save</span>
<span class="hljs-keyword">var</span> spaceShip = Synergykit.Data(<span class="hljs-string">"SpaceShips"</span>);

<span class="hljs-comment">// Set any properities you want</span>
spaceShip.set(<span class="hljs-string">"type"</span>, <span class="hljs-string">"Star Fighter"</span>);
spaceShip.set(<span class="hljs-string">"code"</span>, <span class="hljs-string">"ARC-170"</span>);
spaceShip.set(<span class="hljs-string">"description"</span>, <span class="hljs-string">"Protecting the skies over Republic worlds were specialized clone fighter forces flying the latest in starfighter technology."</span>);

<span class="hljs-comment">// And save data to SynergyKit</span>
spaceShip.save({
    success: <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">(spaceShip, statusCode)</span> {</span>
        callback(spaceShip);
    },
    error: callback
});




<span class="xml"><span class="hljs-tag">&lt;<span class="hljs-title">div</span> <span class="hljs-attribute">class</span>=<span class="hljs-value">"se-preview-section-delimiter"</span>&gt;</span><span class="hljs-tag">&lt;/<span class="hljs-title">div</span>&gt;</span>
</span></code></pre>

<p>In Cloud Code there are some prepare functions to work with.</p>

<table>
<thead>
<tr>
  <th align="left">Function</th>
  <th>Description</th>
</tr>
</thead>
<tbody><tr>
  <td align="left"><code>log(message)</code></td>
  <td>Save message to logs in administration and also in console</td>
</tr>
<tr>
  <td align="left"><code>console.log(message)</code></td>
  <td>Log message in console</td>
</tr>
<tr>
  <td align="left"><code>callback(result, statusCode)</code></td>
  <td>Return <code>result</code> in response with <code>statusCode</code> defined. By default, <code>result</code> is <code>{}</code> and <code>statusCode</code> is <code>200</code></td>
</tr>
<tr>
  <td align="left"><code>require(module)</code></td>
  <td>Require availible modules listed below</td>
</tr>
</tbody></table>


<p>You have also access to request body in variable params or parameters.</p>

<h3 id="modules">Modules</h3>

<p>Cloud Code runs in the Node.js jailed sandbox and uses strict JavaScript language with some prepared modules and variables, which you can use for your development. You have access to Node.js SDK in Cloud Code and modules which can be require.</p>

<h4 id="momentjs">Moment.js</h4>

<pre class="prettyprint"><code class="language-javascript hljs "><span class="hljs-keyword">var</span> moment = <span class="hljs-built_in">require</span>(<span class="hljs-string">'moment'</span>);
callback(moment);




<span class="xml"><span class="hljs-tag">&lt;<span class="hljs-title">div</span> <span class="hljs-attribute">class</span>=<span class="hljs-value">"se-preview-section-delimiter"</span>&gt;</span><span class="hljs-tag">&lt;/<span class="hljs-title">div</span>&gt;</span>
</span></code></pre>

<h4 id="request">Request</h4>

<pre class="prettyprint"><code class="language-javascript hljs "><span class="hljs-keyword">var</span> request = <span class="hljs-built_in">require</span>(<span class="hljs-string">'request'</span>);
request.get({
    uri: <span class="hljs-string">"https://demo.api.synergykit.com/v2.1"</span>
}, <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">(err, response, result)</span> {</span>
    callback(result)
})





&lt;div <span class="hljs-keyword">class</span>=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;<span class="xml"><span class="hljs-tag">&lt;/<span class="hljs-title">div</span>&gt;</span>
</span></code></pre>

<h4 id="underscorejs">Underscore.js</h4>

<pre class="prettyprint"><code class="language-javascript hljs "><span class="hljs-keyword">var</span> _ = <span class="hljs-built_in">require</span>(<span class="hljs-string">"underscore"</span>);
callback(_.isString(params.name));




<span class="xml"><span class="hljs-tag">&lt;<span class="hljs-title">div</span> <span class="hljs-attribute">class</span>=<span class="hljs-value">"se-preview-section-delimiter"</span>&gt;</span><span class="hljs-tag">&lt;/<span class="hljs-title">div</span>&gt;</span>
</span></code></pre>

<h4 id="urlify">Urlify</h4>

<pre class="prettyprint"><code class="language-javascript hljs "><span class="hljs-keyword">var</span> urlify = <span class="hljs-built_in">require</span>(<span class="hljs-string">"urlify"</span>).create({
    spaces: <span class="hljs-string">"-"</span>,
    nonPrintable: <span class="hljs-string">"-"</span>,
    toLower: <span class="hljs-literal">true</span>,
    trim: <span class="hljs-literal">true</span>
});
callback(urlify(params.fullname));




<span class="xml"><span class="hljs-tag">&lt;<span class="hljs-title">div</span> <span class="hljs-attribute">class</span>=<span class="hljs-value">"se-preview-section-delimiter"</span>&gt;</span><span class="hljs-tag">&lt;/<span class="hljs-title">div</span>&gt;</span>
</span></code></pre>

<h3 id="run-cloud-code">Run cloud code</h3>

<p>To run cloud code, you need to specify function first. For this example lets use the prepared function in administration called Example, under section Cloud Code.</p>

<p>To run function, send <strong>POST</strong> request to</p>

<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/functions/example




&lt;div class=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/div&gt;
</code></pre>

<p><strong>Curl example</strong></p>

<pre class="prettyprint"><code class="language-text hljs avrasm">curl -<span class="hljs-built_in">X</span> POST \
-H <span class="hljs-string">"Content-Type: application/json"</span> \
-H <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
<span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/functions/example




&lt;div class=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/div&gt;
</code></pre>

<p>Response will be JSON object sent in callback function.</p>

<h2 id="batch-request">Batch request</h2>

<p>To reduce the amount of time spent on network round trips, you can get, create, update, or delete up to 50 objects in one call, using the batch endpoint.</p>

<h3 id="using-batch">Using batch</h3>

<p>Each command in a batch has id, method, endpoint, and body parameters that specify the HTTP command that would normally be used for that command. The commands are run in the order they are given. For example, to create a couple of example objects, send <strong>POST</strong> request to</p>

<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/batch




&lt;div class=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/div&gt;
</code></pre>

<p><strong>Curl example</strong></p>

<pre class="prettyprint"><code class="language-text hljs fsharp">curl -X POST \
-H <span class="hljs-string">"Content-Type: application/json"</span> \
-H <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
-d '[
        {
            <span class="hljs-string">"id"</span>: <span class="hljs-number">1</span>,
            <span class="hljs-string">"method"</span>: <span class="hljs-string">"POST"</span>,
            <span class="hljs-string">"endpoint"</span>: <span class="hljs-string">"/data/example"</span>,
            <span class="hljs-string">"body"</span>: {
                <span class="hljs-string">"name"</span>: <span class="hljs-string">"Anakin Skywalker"</span>,
                <span class="hljs-string">"lightsaber"</span>: <span class="hljs-string">"blue"</span>
            }
        },
        {
            <span class="hljs-string">"id"</span>: <span class="hljs-number">2</span>,
            <span class="hljs-string">"method"</span>: <span class="hljs-string">"POST"</span>,
            <span class="hljs-string">"endpoint"</span>: <span class="hljs-string">"/data/example"</span>,
            <span class="hljs-string">"body"</span>: {
                <span class="hljs-string">"name"</span>: <span class="hljs-string">"Darth Vader"</span>,
                <span class="hljs-string">"lightsaber"</span>: <span class="hljs-string">"red"</span>
            }
        }
    ]' \
https:<span class="hljs-comment">//demo.api.synergykit.com/v2.1/batch</span>




&lt;div <span class="hljs-keyword">class</span>=<span class="hljs-string">"se-preview-section-delimiter"</span>&gt;&lt;/div&gt;
</code></pre>

<p>Response will be array of JSON objects.</p>

<pre class="prettyprint"><code class="language-json hljs ">[{
    "<span class="hljs-attribute">id</span>": <span class="hljs-value"><span class="hljs-number">1</span></span>,
    "<span class="hljs-attribute">statusCode</span>": <span class="hljs-value"><span class="hljs-number">200</span></span>,
    "<span class="hljs-attribute">body</span>": <span class="hljs-value">{
        "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">0</span></span>,
        "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1430312287559</span></span>,
        "<span class="hljs-attribute">user_ids</span>": <span class="hljs-value">[<span class="hljs-string">"anonymous"</span>]</span>,
        "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"12a09916-16d9-427c-8eff-be0d4b68777e"</span></span>,
        "<span class="hljs-attribute">name</span>": <span class="hljs-value"><span class="hljs-string">"Anakin Skywalker"</span></span>,
        "<span class="hljs-attribute">lightsaber</span>": <span class="hljs-value"><span class="hljs-string">"blue"</span></span>,
        "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1430312287559</span>
    </span>}
</span>}, {
    "<span class="hljs-attribute">id</span>": <span class="hljs-value"><span class="hljs-number">2</span></span>,
    "<span class="hljs-attribute">statusCode</span>": <span class="hljs-value"><span class="hljs-number">200</span></span>,
    "<span class="hljs-attribute">body</span>": <span class="hljs-value">{
        "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">0</span></span>,
        "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1430312288499</span></span>,
        "<span class="hljs-attribute">user_ids</span>": <span class="hljs-value">[<span class="hljs-string">"anonymous"</span>]</span>,
        "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"8cc3079b-40e2-4e1a-95d1-e7b97f216c60"</span></span>,
        "<span class="hljs-attribute">name</span>": <span class="hljs-value"><span class="hljs-string">"Darth Vader"</span></span>,
        "<span class="hljs-attribute">lightsaber</span>": <span class="hljs-value"><span class="hljs-string">"red"</span></span>,
        "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1430312288499</span>
    </span>}
</span>}]</code></pre>

<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/users/me/platforms/<span class="hljs-number">2393265</span>f-cfee-<span class="hljs-number">429</span>a-ad042fbd1b126d</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs haml">curl -X DELETE \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>https://demo.api.synergykit.com/v2.1/users/me/platforms/2393265f-cfee-429a-ad04-3d2fbd1b126d</code></pre>

<p>The response body will contain an empty JSON object.</p>

<h3 id="linking-users-1">Linking users</h3>

<p>SynergyKit allows you to link your users with services like Twitter, Facebook and Google+, enabling your users to sign up or log into your application using their existing identities. This is accomplished through the sign-up REST endpoint by providing authentication data for the service you wish to link to a user in the authData field. Once your user is associated with a service, the authData for the service will be stored with the user and is retrievable by logging in.</p>

<p>authData is a JSON object with keys for each linked service containing the data below. In each case, you are responsible for completing the authentication flow (e.g. OAuth 1.0a) to obtain the information the the service requires for linking.</p>



<h4 id="facebook-authdata-1">Facebook authData</h4>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">facebook</span>": <span class="hljs-value">{
        "<span class="hljs-attribute">id</span>": <span class="hljs-value"><span class="hljs-string">"user's Facebook id number as a string"</span></span>,
        "<span class="hljs-attribute">access_token</span>": <span class="hljs-value"><span class="hljs-string">"an authorized Facebook access token for the user"</span>
    </span>}
</span>}</code></pre>



<h4 id="twitter-authdata-1">Twitter authData</h4>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">twitter</span>": <span class="hljs-value">{
        "<span class="hljs-attribute">id</span>": <span class="hljs-value"><span class="hljs-string">"user's Twitter id number as a string"</span></span>,
        "<span class="hljs-attribute">screen_name</span>": <span class="hljs-value"><span class="hljs-string">"user's Twitter screen name"</span></span>,
        "<span class="hljs-attribute">consumer_key</span>": <span class="hljs-value"><span class="hljs-string">"your application's consumer key"</span></span>,
        "<span class="hljs-attribute">consumer_secret</span>": <span class="hljs-value"><span class="hljs-string">"your application's consumer secret"</span></span>,
        "<span class="hljs-attribute">auth_token</span>": <span class="hljs-value"><span class="hljs-string">"an authorized Twitter token for the user with your application"</span></span>,
        "<span class="hljs-attribute">auth_token_secret</span>": <span class="hljs-value"><span class="hljs-string">"the secret associated with the auth_token"</span>
    </span>}
</span>}</code></pre>



<h4 id="google-authdata-1">Google+ authData</h4>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">google</span>": <span class="hljs-value">{
        "<span class="hljs-attribute">id</span>": <span class="hljs-value"><span class="hljs-string">"user's Google+ id number as a string"</span>
    </span>}
</span>}</code></pre>



<h4 id="anonymous-authdata-1">Anonymous authData</h4>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">anonymous</span>": <span class="hljs-value">{}
</span>}</code></pre>



<h4 id="signing-up-and-logging-in-1">Signing Up and Logging In</h4>

<p>Signing a user up with a linked service and logging them in with that service uses the same <strong>POST</strong> request, in which the authData for the user is specified. For example, to sign up or log in with a user’s Facebook account:</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/users</code></pre>

<p><strong>Curl Example</strong></p>



<pre class="prettyprint"><code class="language-text hljs scilab">curl -X POST \
-H <span class="hljs-string">"Content-Type: application/json"</span> \
-H <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
-d <span class="hljs-string">'{
    "</span>authData<span class="hljs-string">": {
        "</span>facebook<span class="hljs-string">": {
                "</span>id<span class="hljs-string">": "</span><span class="hljs-number">12345678</span><span class="hljs-string">",
                "</span>access_token<span class="hljs-string">": "</span>zIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwY<span class="hljs-string">",
            }
        }
    }'</span> \
https:<span class="hljs-comment">//demo.api.synergykit.com/v2.1/users</span></code></pre>

<p>The new user or logged user will be returned.</p>

<p><strong>Response body</strong></p>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"2dba8954-0c42-46d0-9dad-90f9236a4774"</span></span>,
    "<span class="hljs-attribute">isActivated</span>": <span class="hljs-value"><span class="hljs-literal">true</span></span>,
    "<span class="hljs-attribute">sessionToken</span>": <span class="hljs-value"><span class="hljs-string">"QxNi1iMzEwYWQzMmQyOGzowMzIwN"</span></span>,
    "<span class="hljs-attribute">platforms</span>": <span class="hljs-value">[]</span>,
    "<span class="hljs-attribute">roles</span>": <span class="hljs-value">[]</span>,
    "<span class="hljs-attribute">authData</span>": <span class="hljs-value">{
        "<span class="hljs-attribute">facebook</span>": <span class="hljs-value">{
            "<span class="hljs-attribute">id</span>": <span class="hljs-value"><span class="hljs-string">"12345678"</span></span>,
            "<span class="hljs-attribute">access_token</span>": <span class="hljs-value"><span class="hljs-string">"zIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwY"</span></span>,
        }
    </span>}</span>,
    "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1418145026788</span></span>,
    "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1418143678670</span></span>,
    "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">1</span></span>,
}</code></pre>



<h2 id="communication-1">Communication</h2>

<p>In SynergyKit you can communicate with your users by different ways. There are listed some methods below this section.</p>

<p>One way is to sending push notifications into user devices. This action need to have filled your API key for Android devices in Settings, section Android. For push notifications into iOS devices you need to fill your password and certificates into Apple section in Settings.</p>

<p>Another way is to sending emails to your users. For this you need to create email templates in administration under Mailing section.</p>



<h3 id="send-notification-1">Send notification</h3>

<p>To send push notification to users, send a <strong>POST</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/users/notification</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs haml">curl -X POST \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>-<span class="ruby">d <span class="hljs-string">'{"userIds": "65fcc878-1f87-478f-851e-a0aaedade8b2", "alert": "Use the force!"}'</span> \
</span>https://demo.api.synergykit.com/v2.1/users/notification</code></pre>

<table>
<thead>
<tr>
  <th align="left">Parameter</th>
  <th align="left">Type</th>
  <th>Description</th>
  <th align="left"></th>
</tr>
</thead>
<tbody><tr>
  <td align="left">userIds</td>
  <td align="left">String or Array of Strings</td>
  <td>IDs of user(s) which you want send push notification.</td>
  <td align="left"><strong>required</strong></td>
</tr>
<tr>
  <td align="left">alert</td>
  <td align="left">String</td>
  <td>Message which will be shown in notification bar.</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">sound</td>
  <td align="left">String</td>
  <td>Sound to play on target device. (Works on iOS devices only).</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">badge</td>
  <td align="left">String</td>
  <td>The number which will be shown in badge. (Works on iOS devices only).</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">payload</td>
  <td align="left">String</td>
  <td>Additional data. (Works on iOS devices only).</td>
  <td align="left"></td>
</tr>
</tbody></table>


<p>The response body will contain an empty JSON object.</p>



<h3 id="send-e-mail-1">Send e-mail</h3>

<p>To send email, you need to specify template first. For this example lets use the prepared template in administration called Example, under section Mailing.</p>

<p>To send email, send <strong>POST</strong> request to </p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/mail/example</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs scilab">curl -X POST \
-H <span class="hljs-string">"Content-Type: application/json"</span> \
-H <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
-d <span class="hljs-string">'{"</span>subject<span class="hljs-string">": "</span>Hello Anakin<span class="hljs-string">", "</span>email<span class="hljs-string">": "</span>anakin@<span class="hljs-transposed_variable">tatooine.</span>planet<span class="hljs-string">", "</span>name<span class="hljs-string">": "</span>Anakin<span class="hljs-string">"}'</span> \
https:<span class="hljs-comment">//demo.api.synergykit.com/v2.1/mail/example</span></code></pre>

<p>The response body will contain an empty JSON object.</p>



<h2 id="files-1">Files</h2>

<p>SynergyKit can be also used for storing as much quantity of files as you need for your application.</p>



<h3 id="upload-file-1">Upload file</h3>

<p>To upload a file to SynergyKit, send a <strong>POST</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/files</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs haml">curl -X POST \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: multipart/form-data"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>-<span class="ruby"><span class="hljs-constant">F</span> <span class="hljs-string">"filedata=@test_image.jpg"</span> \
</span>https://demo.api.synergykit.com/v2.1/files</code></pre>

<p>The response body will containt JSON object.</p>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">0</span></span>,
    "<span class="hljs-attribute">size</span>": <span class="hljs-value"><span class="hljs-number">294119</span></span>,
    "<span class="hljs-attribute">extension</span>": <span class="hljs-value"><span class="hljs-string">"jpg"</span></span>,
    "<span class="hljs-attribute">path</span>": <span class="hljs-value"><span class="hljs-string">"https://synergykit.blob.core.windows.net/demo/ad2806dc5d9f5f86656c43cd95156bcf.jpg"</span></span>,
    "<span class="hljs-attribute">filename</span>": <span class="hljs-value"><span class="hljs-string">"ad2806dc5d9f5f86656c43cd95156bcf.jpg"</span></span>,
    "<span class="hljs-attribute">applicationUrl</span>": <span class="hljs-value"><span class="hljs-string">"demo"</span></span>,
    "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1421507284342</span></span>,
    "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1421507284342</span></span>,
    "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"62fc07ea-9123-443c-ac66-c1eaa627a4a9"</span>
</span>}</code></pre>



<h3 id="retrieve-file-by-id-1">Retrieve file by ID</h3>

<p>To retrieve a file by ID, send a <strong>GET</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/files/<span class="hljs-number">62</span>fc07ea-<span class="hljs-number">9123</span>-<span class="hljs-number">443</span>c-ac66-c1eaa627a4a9</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs haml">curl -X GET \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>https://demo.api.synergykit.com/v2.1/files/62fc07ea-9123-443c-ac66-c1eaa627a4a9</code></pre>

<p>The response body will containt JSON object.</p>



<pre class="prettyprint"><code class="language-json hljs ">{
    "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">0</span></span>,
    "<span class="hljs-attribute">size</span>": <span class="hljs-value"><span class="hljs-number">294119</span></span>,
    "<span class="hljs-attribute">extension</span>": <span class="hljs-value"><span class="hljs-string">"jpg"</span></span>,
    "<span class="hljs-attribute">path</span>": <span class="hljs-value"><span class="hljs-string">"https://synergykit.blob.core.windows.net/demo/ad2806dc5d9f5f86656c43cd95156bcf.jpg"</span></span>,
    "<span class="hljs-attribute">filename</span>": <span class="hljs-value"><span class="hljs-string">"ad2806dc5d9f5f86656c43cd95156bcf.jpg"</span></span>,
    "<span class="hljs-attribute">applicationUrl</span>": <span class="hljs-value"><span class="hljs-string">"demo"</span></span>,
    "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1421507284342</span></span>,
    "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1421507284342</span></span>,
    "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"62fc07ea-9123-443c-ac66-c1eaa627a4a9"</span>
</span>}</code></pre>



<h3 id="delete-file-1">Delete file</h3>

<p>To delete file, send a <strong>DELETE</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/files/<span class="hljs-number">62</span>fc07ea-<span class="hljs-number">9123</span>-<span class="hljs-number">443</span>c-ac66-c1eaa627a4a9</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs haml">curl -X DELETE \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>https://demo.api.synergykit.com/v2.1/files/62fc07ea-9123-443c-ac66-c1eaa627a4a9</code></pre>

<p>The response body will contain an empty JSON object.</p>



<h2 id="cloud-code-1">Cloud Code</h2>

<p>Our vision is to let developers build any app without dealing with servers. For complex apps, sometimes you just need a bit of logic that isn’t running on a mobile device. Cloud Code makes this possible.</p>

<p><strong>Cloud Code example</strong></p>



<pre class="prettyprint"><code class="language-javascript hljs "><span class="hljs-comment">// Create instance of Data object and as first parameter specify the collection where to save</span>
<span class="hljs-keyword">var</span> spaceShip = Synergykit.Data(<span class="hljs-string">"SpaceShips"</span>);

<span class="hljs-comment">// Set any properities you want</span>
spaceShip.set(<span class="hljs-string">"type"</span>, <span class="hljs-string">"Star Fighter"</span>);
spaceShip.set(<span class="hljs-string">"code"</span>, <span class="hljs-string">"ARC-170"</span>);
spaceShip.set(<span class="hljs-string">"description"</span>, <span class="hljs-string">"Protecting the skies over Republic worlds were specialized clone fighter forces flying the latest in starfighter technology."</span>);

<span class="hljs-comment">// And save data to SynergyKit</span>
spaceShip.save({
    success: <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">(spaceShip, statusCode)</span> {</span>
        callback(spaceShip);
    },
    error: callback
});</code></pre>

<p>In Cloud Code there are some prepare functions to work with.</p>

<table>
<thead>
<tr>
  <th align="left">Function</th>
  <th>Description</th>
</tr>
</thead>
<tbody><tr>
  <td align="left"><code>log(message)</code></td>
  <td>Save message to logs in administration and also in console</td>
</tr>
<tr>
  <td align="left"><code>console.log(message)</code></td>
  <td>Log message in console</td>
</tr>
<tr>
  <td align="left"><code>callback(result, statusCode)</code></td>
  <td>Return <code>result</code> in response with <code>statusCode</code> defined. By default, <code>result</code> is <code>{}</code> and <code>statusCode</code> is <code>200</code></td>
</tr>
<tr>
  <td align="left"><code>require(module)</code></td>
  <td>Require availible modules listed below</td>
</tr>
</tbody></table>


<p>You have also access to request body in variable params or parameters.</p>



<h3 id="modules-1">Modules</h3>

<p>Cloud Code runs in the Node.js jailed sandbox and uses strict JavaScript language with some prepared modules and variables, which you can use for your development. You have access to Node.js SDK in Cloud Code and modules which can be require.</p>



<h4 id="momentjs-1">Moment.js</h4>



<pre class="prettyprint"><code class="language-javascript hljs "><span class="hljs-keyword">var</span> moment = <span class="hljs-built_in">require</span>(<span class="hljs-string">'moment'</span>);
callback(moment);</code></pre>



<h4 id="request-1">Request</h4>



<pre class="prettyprint"><code class="language-javascript hljs "><span class="hljs-keyword">var</span> request = <span class="hljs-built_in">require</span>(<span class="hljs-string">'request'</span>);
request.get({
    uri: <span class="hljs-string">"https://demo.api.synergykit.com/v2.1"</span>
}, <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">(err, response, result)</span> {</span>
    callback(result)
})</code></pre>

<h4 id="underscorejs-1">Underscore.js</h4>



<pre class="prettyprint"><code class="language-javascript hljs "><span class="hljs-keyword">var</span> _ = <span class="hljs-built_in">require</span>(<span class="hljs-string">"underscore"</span>);
callback(_.isString(params.name));</code></pre>



<h4 id="urlify-1">Urlify</h4>



<pre class="prettyprint"><code class="language-javascript hljs "><span class="hljs-keyword">var</span> urlify = <span class="hljs-built_in">require</span>(<span class="hljs-string">"urlify"</span>).create({
    spaces: <span class="hljs-string">"-"</span>,
    nonPrintable: <span class="hljs-string">"-"</span>,
    toLower: <span class="hljs-literal">true</span>,
    trim: <span class="hljs-literal">true</span>
});
callback(urlify(params.fullname));</code></pre>



<h3 id="run-cloud-code-1">Run cloud code</h3>

<p>To run cloud code, you need to specify function first. For this example lets use the prepared function in administration called Example, under section Cloud Code.</p>

<p>To run function, send <strong>POST</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/functions/example</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs haml">curl -X POST \
-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Content-Type: application/json"</span> \
</span>-<span class="ruby"><span class="hljs-constant">H</span> <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
</span>https://demo.api.synergykit.com/v2.1/functions/example</code></pre>

<p>Response will be JSON object sent in callback function.</p>



<h2 id="batch-request-1">Batch request</h2>

<p>To reduce the amount of time spent on network round trips, you can get, create, update, or delete up to 50 objects in one call, using the batch endpoint.</p>



<h3 id="using-batch-1">Using batch</h3>

<p>Each command in a batch has id, method, endpoint, and body parameters that specify the HTTP command that would normally be used for that command. The commands are run in the order they are given. For example, to create a couple of example objects, send <strong>POST</strong> request to</p>



<pre class="prettyprint"><code class="language-url hljs avrasm"><span class="hljs-label">https:</span>//demo<span class="hljs-preprocessor">.api</span><span class="hljs-preprocessor">.synergykit</span><span class="hljs-preprocessor">.com</span>/v2<span class="hljs-number">.1</span>/batch</code></pre>

<p><strong>Curl example</strong></p>



<pre class="prettyprint"><code class="language-text hljs scilab">curl -X POST \
-H <span class="hljs-string">"Content-Type: application/json"</span> \
-H <span class="hljs-string">"Authorization: Basic ZGVtbzowMzIwNjI5OS05MzdiLTQ0YzMtODQxNi1iMzEwYWQzMmQyOGI="</span> \
-d <span class="hljs-string">'[
        {
            "</span>id<span class="hljs-string">": 1,
            "</span>method<span class="hljs-string">": "</span>POST<span class="hljs-string">",
            "</span>endpoint<span class="hljs-string">": "</span>/data/example<span class="hljs-string">",
            "</span>body<span class="hljs-string">": {
                "</span>name<span class="hljs-string">": "</span>Anakin Skywalker<span class="hljs-string">",
                "</span>lightsaber<span class="hljs-string">": "</span>blue<span class="hljs-string">"
            }
        },
        {
            "</span>id<span class="hljs-string">": 2,
            "</span>method<span class="hljs-string">": "</span>POST<span class="hljs-string">",
            "</span>endpoint<span class="hljs-string">": "</span>/data/example<span class="hljs-string">",
            "</span>body<span class="hljs-string">": {
                "</span>name<span class="hljs-string">": "</span>Darth Vader<span class="hljs-string">",
                "</span>lightsaber<span class="hljs-string">": "</span>red<span class="hljs-string">"
            }
        }
    ]'</span> \
https:<span class="hljs-comment">//demo.api.synergykit.com/v2.1/batch</span></code></pre>

<p>Response will be array of JSON objects.</p>



<pre class="prettyprint"><code class="language-json hljs ">[{
    "<span class="hljs-attribute">id</span>": <span class="hljs-value"><span class="hljs-number">1</span></span>,
    "<span class="hljs-attribute">statusCode</span>": <span class="hljs-value"><span class="hljs-number">200</span></span>,
    "<span class="hljs-attribute">body</span>": <span class="hljs-value">{
        "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">0</span></span>,
        "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1430312287559</span></span>,
        "<span class="hljs-attribute">user_ids</span>": <span class="hljs-value">[<span class="hljs-string">"anonymous"</span>]</span>,
        "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"12a09916-16d9-427c-8eff-be0d4b68777e"</span></span>,
        "<span class="hljs-attribute">name</span>": <span class="hljs-value"><span class="hljs-string">"Anakin Skywalker"</span></span>,
        "<span class="hljs-attribute">lightsaber</span>": <span class="hljs-value"><span class="hljs-string">"blue"</span></span>,
        "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1430312287559</span>
    </span>}
</span>}, {
    "<span class="hljs-attribute">id</span>": <span class="hljs-value"><span class="hljs-number">2</span></span>,
    "<span class="hljs-attribute">statusCode</span>": <span class="hljs-value"><span class="hljs-number">200</span></span>,
    "<span class="hljs-attribute">body</span>": <span class="hljs-value">{
        "<span class="hljs-attribute">__v</span>": <span class="hljs-value"><span class="hljs-number">0</span></span>,
        "<span class="hljs-attribute">createdAt</span>": <span class="hljs-value"><span class="hljs-number">1430312288499</span></span>,
        "<span class="hljs-attribute">user_ids</span>": <span class="hljs-value">[<span class="hljs-string">"anonymous"</span>]</span>,
        "<span class="hljs-attribute">_id</span>": <span class="hljs-value"><span class="hljs-string">"8cc3079b-40e2-4e1a-95d1-e7b97f216c60"</span></span>,
        "<span class="hljs-attribute">name</span>": <span class="hljs-value"><span class="hljs-string">"Darth Vader"</span></span>,
        "<span class="hljs-attribute">lightsaber</span>": <span class="hljs-value"><span class="hljs-string">"red"</span></span>,
        "<span class="hljs-attribute">updatedAt</span>": <span class="hljs-value"><span class="hljs-number">1430312288499</span>
    </span>}
</span>}]</code></pre>