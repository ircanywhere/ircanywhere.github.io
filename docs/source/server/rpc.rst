RPCHandler
==========

*(c) 2013-2014 http://ircanywhere.com*

**Author:** Ricki Hastings

IRCAnywhere server/rpc.js
 
.. js:class:: RPCHandler.RPCHandler()

   Singleton class to handle the inbound and outbound RPC calls on the websocket lines

   :returns: void

.. js:function:: RPCHandler.init()

   Called when the application is ready, sets up an observer on our collections
   so we can figure out whether we need to propogate them to clients.

   :returns: void

.. js:function:: RPCHandler.push(uid, command, data)

   Pushes the data and command out to any sockets associated to that uid

   :param string uid: A valid user id converted from an object ID
   :param string command: The command to send
   :param string data: The json data to send
   :returns: void

.. js:function:: RPCHandler.handleUsersUpdate(doc)

   Handles any update changes to the users collection and sends changes to clients

   :param object doc: A valid MongoDB document with an _id
   :returns: void

.. js:function:: RPCHandler.handleNetworksAll(doc)

   Handles any all changes to the network collection

   :param object doc: A valid MongoDB document with an _id
   :returns: void

.. js:function:: RPCHandler.handleTabsAll(doc)

   Handles all changes to the tabs collections

   :param object doc: A valid MongoDB document with an _id
   :returns: void

.. js:function:: RPCHandler.handleEventsAll(doc)

   Handles any changes to the events collection

   :param object doc: A valid MongoDB document with an _id
   :returns: void

.. js:function:: RPCHandler.handleCommandsAll(doc)

   Handles all operations on the commands collection

   :param object doc: A valid MongoDB document with an _id
   :returns: void

.. js:function:: RPCHandler.handleChannelUsersAll(doc)

   Handles any changes on the channelUsers collection

   :param object doc: A valid MongoDB document with an _id
   :returns: void

.. js:function:: RPCHandler.onSocketOpen(socket)

   Handles a new websocket opening and attaches the RPC events

   :param object socket: A valid sock.js socket
   :returns: void

.. js:function:: RPCHandler.handleAuth(socket, data)

   Handles the authentication command sent to us from websocket clients
   Authenticates us against login tokens in the user record, disconnects
   if expired or incorrect.

   :param object socket: A valid sock.js socket
   :param object data: A valid data object from sock.js
   :returns: void

.. js:function:: RPCHandler.handleConnect(socket)

   Handles new websocket clients, this is only done after
   they have been authenticated and it's been accepted.

   :param object socket: A valid sock.js socket
   :returns: void

.. js:function:: RPCHandler.handleCommand(socket, data, exec)

   Handles the exec command RPC call. Which should be used to execute /commands
   from the clientside without inserting them into the backlog.

   :param object socket: A valid sock.js socket
   :param object data: A valid data object from sock.js
   :param boolean exec: Whether to exec the command or backlog it
   :returns: void

.. js:function:: RPCHandler.handleReadEvents(socket, data)

   Handles the command which marks events as read. It takes a MongoDB query and updates
   them with that query.

   :param object socket: A valid sock.js socket
   :param object data: A valid data object from sock.js
   :returns: void

.. js:function:: RPCHandler.handleSelectTab(socket, data)

   Handles the selectTab command which is used to change the currently active tab
   for that user.

   :param object socket: A valid sock.js socket
   :param object data: A valid data object from sock.js
   :returns: void

.. js:function:: RPCHandler.handleUpdateTab(socket, data)

   Handles the update tab command, we're allowed to change client side only settings here
   ``hiddenUsers`` and ``hiddenEvents`` only at the moment.

   :param object socket: A valid sock.js socket
   :param object data: A valid data object from sock.js
   :returns: void

.. js:function:: RPCHandler.handleInsertTab(socket, data)

   Allows users to create new tabs on the fly from the client side. Restricted to ``channel`` and ``query`` tabs.

   :param object socket: A valid sock.js socket
   :param object data: A valid data object from sock.js
   :returns: void

.. js:function:: RPCHandler.handleGetEvents(socket, data)

   Handles queries to the events collection

   :param object socket: A valid sock.js socket
   :param object data: A valid data object from sock.js
   :returns: void