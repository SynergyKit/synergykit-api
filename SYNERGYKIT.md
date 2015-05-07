#How SynergyKit Works
[toc]
##SynergyKit

Building an application is complex work which never ends. Nearly every app needs a database, an API, a push notifications and authentication. With SynergyKit — all of this is done for you. Our goal at SynergyKit is to enable you to focus on what you love, not what you are frustrated from.

##Applications

The base of SynergyKit is an application. You can create new application from developer dashboard or from the application list section. You can have how many applications you want. Creating an application you get access to its options and settings.

###Dashboard

On dashboard of application you can see important statistics about usage. There are overviews of requests, traffic, users, file storage and database storage. You can modify filter to another view, per day, per month and per year.

###Settings

There you can find all settings of application.

####General

In this section you can edit the name and description of your application.

####Variants

There you can set variant of your application. You can find details of pricing [here](https://synergykit.com/pricing).

####Android GCM

If you want to send a push notifications to Android devices, you need to specify GCM API key in this section.

####Apple APNs

If you want to send a push notifications to Apple devices, you need to specify details of certificates and password in this section.

### Security

As your app development progresses, you will want to use SynergyKit's security features in order to safeguard your data. This section explains the ways you can secure your apps.

If your app is compromised, it's not only you as the developer who suffers, but potentially the users of your app as well. Continue reading for our suggestions for sensible defaults and precautions to take before releasing your app into the wild.

####Application keys

In this section you can find an application keys for your application and you can also manage them. 
There are two types of keys. The Master key and client keys. All keys can be deleted, except the master key. 

Client keys are shipped as a part of your app, and anyone can decompile your app or proxy network traffic from their device to find your client key. This exploit is even easier with JavaScript — one can simply "view source" in the browser and immediately find your client key.

This is why SynergyKit has many other security features to help you secure your data. The client key is given out to your users, so anything that can be done with just the client key is doable by the general public, even malicious hackers.

On the other hand, the Master key is definitely a security mechanism. Master key is like having root access to your app's servers. You should guard your master key as your root password.

####Roles

As your app is getting larger, you can find useful to get more control over access to your data. SynergyKit supports a form of Role-based Access Control. Roles provide a logical way of grouping users to groups with access privileges to data. Any permission granted to a role is also granted to its users.

We provide a specialized role class to represent these groupings of users for the purposes of assigning permissions. Roles have properties, which are listed below.

|Property|Description|
|:-|-|
|Name|The name of the role will be used as identification. This value is required, and can only be set once as a role is being created. The name must consist of alphanumeric characters, spaces, -, or _.|
|Read|If checked, everyone has read permission.|
|Write|If checked, everyone has write permission.|
|Read only by owner|If checked, only owner of object has read permission to it.|
|Write only by owner|If checked, only owner of the object has write permission.|
|Is default?|If checked, every new user get this role as default.|
|Who can manage?|Specify, who can manage this role.|


In order to keep these roles secure, your mobile apps won't be directly responsible for managing creation and membership of your roles. Roles may be managed by an interface on the web.

####Class Level Permission

Every database collection, users, cloud code, files and mailing section has its own security settings, where you can set roles and their permissions. By default, Public role is set with read and write permission. It means, that anyone has access to everything in this collection. You can change this by adding role and set its permissions.

####Validation schema

Every database collection and users have a validation schema. This schema is JSON schema and its generated after every change made to collection. After you are satisfied with the way it looks, you can lock the schema and it will be checking for submitted data from this moment.

###Developers

In this section you can invite other developers to collaborate on your application. You can find a developer by its name or email. If no developer is found and email address is typed in, the invitation will be send.

###Database

There you can manage your data. The data are saved in collections which are created when the first object is send in. Tehre are some options below which you can do with your collection.

|Name of the action|Description|
|:-|-|
|Export collection|Export your data in JSON file|
|Remove collection|Delete collection and all data in it|
|Remove selected data|Remove only checked data objects|
|Clean collection|Delete data within collection, but leave collection created|
|Edit|Change collection name|

###Users

Users is managed collection. You can see users of application there. There are some options below which you can do with Users collection.

|Name of the action|Description|
|:-|-|
|Export users|Export your data in JSON file|
|Remove all users|Delete all users in this collection|
|Remove selected users|Remove only checked users|

###Logs

There you can see all log activity from your application and your cloud code. There are some options below which you can do with your Logs collection.

|Name of the action|Description|
|:-|-|
|Export logs|Export your data in JSON file|
|Remove all logs|Delete all logs in this collection|

###Cloud Code

Our vision is to let developers build any app without dealing with servers. For complex apps, sometimes you just need a bit of logic that isn't running on a mobile device. Cloud Code makes this possible.

In this section you can write and debug your cloud code right in your favorite browser.

###Application builds

When your application is close to release, you want it to be tested by other people. For this case there is an option to upload your Android .apk file or Apple .ipa file in the form, specify the version and name and share the link to other testers.

###Files

SynergyKit can be also used for saving as much files as you need for your application. You can specify name and upload your file right in the administration or you can use our prepared SDKs.

###Mailing

In this section you can specify an email template in HTML with variables and then send it to your users.