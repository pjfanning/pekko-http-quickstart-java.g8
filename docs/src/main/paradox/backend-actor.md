Backend Actor logic
-------------------

In this example, the backend only uses one basic actor. In a real system, we would have many actors interacting with each other and perhaps, multiple data stores and microservices. 

An interesting side-note to add here is about when using actors in applications like this adds value over just providing functions that would return `CompletionStage`s.
In fact, if your logic is stateless and very simple request/reply style, you may not need to back it with an Actor. Actors do shine however when you need to keep some form of state and allow various requests to access something in (or *through*) an Actor. The other stellar feature of actors, that futures would not handle, is scaling-out onto a cluster very easily, by using @extref[Cluster Sharding](pekko:cluster-sharding.html) or other @extref[location-transparent](pekko:general/remoting.html) techniques.

However, the focus of this tutorial is on how to interact with an Actor backend from within Pekko HTTP -- not on the actor itself, so we'll keep it very simple.
 
The sample code in the `UserRegistry` is very simple. It keeps registered users in a `Set`. Once it receives messages it matches them to the defined cases to determine which action to take:

@@snip [UserRegistry.java]($g8src$/java/$package$/UserRegistry.java) { #user-registry-actor }

If you feel you need to brush up on your Pekko Actor knowledge, the @extref[Getting Started Guide](pekko:guide/index.html) reviews actor concepts in the context of a simple Internet of Things (IoT) example.
