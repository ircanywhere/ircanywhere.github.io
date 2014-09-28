IRCServer
=========

*(c) 2013-2014 http://ircanywhere.com*

**Author:** Rodrigo Silveira

IRCAnywhere server/server.js
 
 .. js:class:: IRCServer.IRCServer()

   This is the IRC server that manages IRC client connections to ircanywhere. The IRC server
   can be turned off by configuration. this is a singleton and should never be instantiated more than once.
    
   The configuration option `ircServer.enable` and `ircServer.port` will control whether this runs and what
   port it runs on. The default port is 6667.

   :returns: void

.. js:function:: IRCServer.init()

   Setup server and start listening for connections.

   :returns: void

.. js:function:: IRCServer.onConnect(socket)

   Handles new server connection. Starts a session.

   :param object socket: Connection socket to the client
   :returns: void