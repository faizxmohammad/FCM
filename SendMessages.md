## Sending Messages to a Topic :

`Sending a message to a topic requires two steps: build a Message object and send it using one of FirebaseMessaging‘s methods`


```Java
Message msg = Message.builder()
  .setTopic(topic)
  .putData("body", "some data")
  .build();
```

Once we have a Message instance, we use send() to request its delivery:

String id = fcm.send(msg);

`Here, fcm is the FirebaseMessaging instance that we've injected into our controller class. send() returns a value which is the FCM-generated message identifier. We can use this identifier for tracking or logging purposes.`

send() also has an asynchronous version, sendAsync(), which returns an ApiFuture object. This class extends Java's Future, so we can easily use it with reactive frameworks like Project Reactor.

## Sending Messages to Specific Clients:

`As we've mentioned before, each client has a unique subscription token associated with it. We use this token as its “address” when building a Message instead of a topic name:`

```Java
Message msg = Message.builder()
  .setToken(registrationToken)
  .putData("body", "some data")
  .build();
```


`For use cases where we want to send the same message to several clients, we can use a MulticastMessage and sendMulticast(). They work the same way as the unicast version but allow us to send the message to up to five hundred clients in a single call:`


```Java
MulticastMessage msg = MulticastMessage.builder()
  .addAllTokens(message.getRegistrationTokens())
  .putData("body", "some data")
  .build();
BatchResponse response = fcm.sendMulticast(msg); 
```

`The returned BatchResponse contains the generated message identifiers and any errors associated with the delivery for a given client.`


## Sending Messages to Multiple Topics:
`FCM allows us to specify a condition to define the intended audience for a message. A condition is a logical expression that selects clients based on topics to which they've subscribed (or not). For instance, given three topics (T1, T2 and T3), this expression targets devices that are subscribers of T1 or T2 but not T3:`

`('T1' in topics || 'T2' in topics) && !('T3' in topics)`

Here, the topics variable represents all topics a given client has subscribed to. We can now build a message addressed to clients that satisfies this condition using the setCondition() method available in the builder:

```Java
    Message msg = Message.builder()
    .setCondition("('T1' in topics || 'T2' in topics) && !('T3' in topics)")
    .putData("body", "some data")
    .build();

    String id = fcm.send(msg);

```


## Subscribing Clients to Topics:


`We use the subscribeToTopic() or its async variant subscribeToTopicAsync() method to create a subscription that associates a client with a topic. The method accepts a list of client registration tokens and a topic name as arguments:`

```Java
`   fcm.subscribeToTopic(registrationTokens, topic);
```
