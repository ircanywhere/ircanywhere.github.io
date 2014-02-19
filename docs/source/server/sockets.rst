SocketManager
=============

*(c) 2013-2014 http://ircanywhere.com*

**Author:** Ricki Hastings

IRCAnywhere server/sockets.js
 
NOTE: I want to rename this to observer/rpc at some point in 0.2.0 final and merge the commands
into a more RPC style which are probably defined in websocket.js, because the majority
of this code is handling the mongo observer stuff and handling allow rules. Little of it
is socket based code, and only a bit of it is socket managing code.
 
I also want to incorporate it all (especially the allow rules) into a more DI based style
where any modules can inject their own RPC methods and allow rules by just putting
items into the prototype (is this possible?) or extend based, for example; ::
 
	CustomModule = _.extend(BaseModule, {
		'allow.collection': {
			insert: function() { ... }
		},
		rpc: {
			mySocketCommand: function() { ... }
		}
	});
 
These would just inject the rpc methods / allow rules into the main RPC manager (this).
Or something similar. I'll spend time ironing out the details at some point
 
.. js:class:: SocketManager.SocketManager()

   Responsible for handling all the websockets and their RPC-style commands

   :returns: void

.. js:attribute:: SocketManager.propogate

   An array of collections to propoagate to the client when changes occur

   :type: array 

.. js:function:: SocketManager.allow(collection, object)

   Responsible for setting allow rules on collection modifications from the client side
   currently only compatible with inserts and updates.

   :param string collection: An existing Mongo collection
   :param object object: An object containing valid operation functions `update` and `insert`
   :returns: void

.. js:function:: SocketManager.rules(collection, object)

   Responsible for setting operation rules on how to update things

   :param string collection: An existing Mongo collection
   :param object object: An object containing valid operation functions `update` and `insert`
   :returns: void

.. js:function:: SocketManager.init()

   Called when the application is ready, sets up an observer on our collections
   so we can figure out whether we need to propogate them to clients and who to.
    
   We also setup the websocket connection handlers and everything relating to that here.

   :returns: void

.. js:function:: SocketManager.onSocketOpen(socket)

   Handles a new websocket opening and attaches the RPC events

   :param object socket: A valid sock.js socket
   :returns: void

.. js:function:: SocketManager.handleAuth(socket, data)

   Handles the authentication command sent to us from websocket clients
   Authenticates us against login tokens in the user record, disconnects
   if expired or incorrect.

   :param object socket: A valid sock.js socket
   :param object data: A valid data object from sock.js
   :returns: void

.. js:function:: SocketManager.handleConnect(socket)

   Handles new websocket clients, this is only done after
   they have been authenticated and it's been accepted.

   :param object socket: A valid sock.js socket
   :returns: void

.. js:function:: SocketManager.handleEvents(socket, data)

   Handles queries to the events collection

   :param object socket: A valid sock.js socket
   :param object data: A valid data object from sock.js
   :returns: void

.. js:function:: SocketManager.handleInsert(socket, data)

   Handles insert rpc calls

   :param object socket: A valid sock.js socket
   :param object data: A valid data object from sock.js
   :returns: void

.. js:function:: SocketManager.handleUpdate(socket, data)

   Handles update rpc calls

   :param object socket: A valid sock.js socket
   :param object data: A valid data object from sock.js
   :returns: void