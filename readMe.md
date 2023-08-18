`Clients`: mobile or web applications(Server send messages to them)

`Topic or subscription-based addressing` : Send messages to all or specific clients 

# FCM Architecture : 

![alt text](https://www.baeldung.com/wp-content/uploads/2022/11/BAEL_5900_Architecture.png)



`Application Servers`: These are the servers owned and managed by the app developer. They initiate message requests to FCM to send notifications to specific devices or device groups. The application servers are responsible for creating and sending messages using the FCM API.

`Firebase Cloud Messaging (FCM) Server`: This is the core component of the FCM architecture. It acts as a central messaging relay between the application servers and the client devices. When an application server sends a message request, the FCM server handles the routing and delivery of the message to the intended recipients.

`Clients (Mobile Apps, Web Apps)`: The client-side components are the mobile apps (Android and iOS) or web apps that are installed on users' devices. These clients have integrated the FCM SDK, which allows them to establish a connection with the FCM server. This SDK enables devices to receive and display notifications and messages from the FCM server.

`Topics and Device Groups`: FCM allows developers to categorize devices into topics or device groups based on certain criteria. Topics are used to send messages to multiple devices that have subscribed to the same topic, while device groups enable sending messages to multiple devices belonging to the same user.

`User Devices`: These are the actual devices used by end-users, such as smartphones, tablets, or web browsers. The FCM SDK integrated into the app on these devices manages the receipt and display of notifications.


### Here's how the process typically works  : 

`Registration`: The mobile app or web app registers with FCM by initializing the FCM SDK and obtaining a unique registration token. This token is used to identify the device and establish a communication channel with the FCM server.

`Token Exchange`: The registration token is sent from the client device to the application server, allowing the server to target specific devices for sending messages.

`Message Sending`: The application server constructs and sends messages using the FCM API. Messages can be targeted to individual devices, topics, or device groups based on the registration tokens.

`Message Routing`: The FCM server receives the message from the application server and uses the provided registration tokens to route the message to the appropriate client devices.

`Message Display`: The FCM SDK on the client devices receives the message from the FCM server and triggers the display of notifications or performs other actions defined by the app developer.

`User Interaction`: When the user interacts with the notification, the app can handle the interaction by launching a specific activity or performing a certain action within the app.



##### In Springboot we are going to use a REST API. This API allows us to explore the different ways we can send notifications to our Applications.

`1. Publish notifications to a topic`
`2. Publish notifications to specific clients`
`3. Publish notifications to multiple topics`


## Topic :

``A topic is a named entity that acts as a hub for notifications that share some properties.``

A topic in FCM is a way to categorize devices and users. It allows you to send a message to multiple devices that have subscribed to a particular topic. Topics are a useful way to broadcast messages to a group of users who share a common interest or belong to a specific category. 

`For example, in a news app, you could have topics like "Sports," "Technology," and "Entertainment." Users who subscribe to these topics will receive relevant notifications.`

To send a message to a topic, you simply specify the topic name as the target when sending the message from the server. Devices that have subscribed to that topic will receive the message.


## Client :
`In FCM, a client refers to an individual instance of a mobile app or a web app installed on a user's device. Each client is uniquely identified by its registration token, which is generated when the app is installed and registered with FCM. This token is used to establish a communication channel between the client app and the FCM server.`

`The client app includes the FCM SDK, which allows it to handle incoming messages and notifications, as well as send registration tokens to the app server for targeting messages.`


###### Note : 
`To receive notifications, a client uses the appropriate SDK API calls to register itself with our Firebase project. Upon successful registration, the client gets a unique registration token from Firebase. Usually, this token is sent to the server side so it can be used for direct notifications.`


## Subscriptions :
`Subscriptions refer to the act of a client or device subscribing to a specific topic. When a client subscribes to a topic, it indicates that it is interested in receiving messages related to that topic. Similarly, a client can unsubscribe from a topic if it no longer wants to receive messages related to that topic.`

`Subscriptions are managed on the client side using the FCM SDK. The client app can subscribe to topics using the provided APIs. On the server side, you can use the FCM API to send messages to the subscribed topics.`

`A subscription represents the association between a client and a topic.`


![alt text](https://firebase.google.com/static/docs/cloud-messaging/images/diagram-FCM.png)