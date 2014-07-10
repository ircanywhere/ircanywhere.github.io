IdentdServer
============

*(c) 2013-2014 http://ircanywhere.com*

**Author:** Ricki Hastings

IRCAnywhere server/identd.js
 
.. js:class:: IdentdServer.IdentdServer()

   This is the IdentdServer object which creates an integrated identd server and can be turned
   off via the configuration, this is a singleton and should never be instantiated more than once.
    
   The configuration option `identd.enable` and `identd.port` will control whether this runs and what port
   it runs on, the default port is 113 but you can bind it to whatever you like and use iptables
   to forward to 113, without doing that IRCAnywhere will need elevated permissions to bind.

   :returns: void

.. js:function:: IdentdServer.init()

   Initiates the identd server and handles any configuration options

   :returns: void

.. js:function:: IdentdServer.onData(socket, data)

   Handles incoming data to the identd server, this shouldn't ever be called, but the documentation is
   here so people know what the function is doing and where responses are handled etc.
   Protocol information can be found at http://en.wikipedia.org/wiki/Ident_protocol

   :param socket socket: A valid socket from net.createServer callback
   :param bufferobject data: http://nodejs.org/api/net.html#net_event_data
   :returns: void

.. js:function:: IdentdServer.parse(line)

   Once the data has been handled it needs to be parsed so we can figure out what the identd request is
   and respond to it accordingly to validate our connecting user.

   :param string line: The parsed ident line
   :returns: The response for the requester