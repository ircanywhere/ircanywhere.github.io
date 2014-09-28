ServerSession
=============

*(c) 2013-2014 http://ircanywhere.com*

**Author:** Rodrigo Silveira

IRCAnywhere server/serversession.js
 
 .. js:function:: .disconnectUser()

   Disconnects the socket.

   :returns: void.. js:class:: ServerSession.ServerSession(socket)

   Handles the communication between an IRC client and ircanywhere's IRC server. Instantiated on
   every new client connection.

   :param object socket: Connection socket to the client
   :returns: void

.. js:attribute:: ServerSession.debug

   A flag to determine whether debug logging is enabled or not

   :type: boolean 

.. js:function:: ServerSession.init()

   Initializes session.

   :returns: void

.. js:function:: ServerSession.pass(message)

   Handles PASS message from client. Stores password for login.

   :param object message: Received message
   :returns: void

.. js:function:: ServerSession.nick(message)

   Handles NICK message from client. If message arrives before welcome, just store nickname temporarily to use
   on the welcome message. Otherwise forward it.

   :param object message: Received message
   :returns: void

.. js:function:: ServerSession.quit()

   Handles QUIT message from client. Disconnects the user.

   :returns: void

.. js:function:: ServerSession.user(message)

   Handles USER message from client. Start login sequence. Username should contain network information if
   more then one network is registered. Username with network is in the form:

   :param object message: Received message
   :returns: void

.. js:function:: ServerSession.setup()

   Sets up client to listen to IRC activity.

   :returns: void

.. js:function:: ServerSession.handleEvent(event)

   Handle IRC events.

   :param object event: Event to handle
   :returns: void

.. js:function:: ServerSession.handleIrcMessage(ircMessage)

   Forwards messages that are not stored in the events collection in the database.

   :param object ircMessage: Irc Message object
   :returns: void

.. js:function:: ServerSession.sendWelcome()

   Sends stored welcome message from network to client. Message order is registered, lusers,
   nick (to set to stored nick), motd and usermode.



.. js:function:: ServerSession.sendJoins()

   Sends to client a join message for each active channel tab.



.. js:function:: ServerSession.sendChannelInfo(tab)

   Sends channel information, such as NAMES, TOPIC etc

   :param object tab: Channel tab
   :returns: void

.. js:function:: ServerSession.sendPlayback()

   Sends playback messages to client.

   :returns: void

.. js:function:: ServerSession.privmsg(message)

   Handles PRIVMSG messages from client. Forwards to ircHandler and to ircFactory.

   :param object message: Received message
   :returns: void

.. js:function:: ServerSession.onClientMessage(message, command)

   Handles all message that do not have a specific handler.

   :param object message: Received message
   :param string command: Messages command
   :returns: void

.. js:function:: ServerSession.sendRaw(rawMessage)

   Sends a raw message to the client

   :param string rawMessage: Raw message
   :returns: void