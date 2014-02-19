WebSocket
=========

*(c) 2013-2014 http://ircanywhere.com*

**Author:** Ricki Hastings

IRCAnywhere server/websocket.js
 
.. js:class:: WebSocket.WebSocket(socket)

   Wrapper for sock.js sockets.

   :param object socket: A valid sock.js socket
   :returns: void

.. js:function:: WebSocket.bindEvents()

   Binds our sock.js events to _socket.

   :returns: void

.. js:function:: WebSocket.isValid(parsed)

   Checks if an incoming message object is valid.

   :param object parsed: An incoming message object to parse
   :returns: Whether the object is valid or not

.. js:function:: WebSocket.onMessage(raw)

   Handles an incoming message.

   :param string raw: A raw line from a sock.js websocket
   :returns: void

.. js:function:: WebSocket.onClose()

   Handles closing the websocket connection.

   :returns: void

.. js:function:: WebSocket.send(event, data[, close])

   Sends outgoing packets

   :param string event: The event to send
   :param object data: The data object to send, should be JSON
   :param boolean [close]: Whether to close the connection after the data has been sent or not
   :returns: void

.. js:function:: WebSocket.sendBurst(data)

   Compiles a temporary GET route and sends it to a socket

   :param object data: The data object to push into a route and send down the socket
   :returns: void