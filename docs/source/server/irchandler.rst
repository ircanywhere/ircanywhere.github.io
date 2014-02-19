IRCHandler
==========

*(c) 2013-2014 http://ircanywhere.com*

**Author:** Ricki Hastings

IRCAnywhere server/irchandler.js
 
.. js:class:: IRCHandler.IRCHandler()

   The object responsible for handling an event from IRCFactory
   none of these should be called directly, however they can be hooked onto
   or have their actions prevented or replaced. The function names equal directly
   to irc-factory events and are case sensitive to them.

   :returns: void

.. js:attribute:: IRCHandler.blacklisted

   An array of blacklisted commands which should be ignored

   :type: array 

.. js:function:: IRCHandler._formatRaw(raw)

   Formats an array of RAW IRC strings, taking off the :leguin.freenode.net 251 ricki- :
   at the start, returns an array of strings with it removed

   :param array raw: An array of raw IRC strings to format
   :returns: A formatted array of the inputted strings

.. js:function:: IRCHandler.registered(client, message)

   Handles the registered event, this will only ever be called when an IRC connection has been
   fully established and we've recieved the `registered` events. This means when we reconnect to
   an already established connection we won't get this event again.

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.closed(client, message)

   Handles a closed connection

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.failed(client, message)

   Handles a failed event, which is emitted when the retry attempts are exhaused

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.lusers(client, message)

   Handles an incoming lusers event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.motd(client, message)

   Handles an incoming motd event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.join(client, message)

   Handles an incoming join event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.part(client, message)

   Handles an incoming part event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.kick(client, message)

   Handles an incoming kick event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.quit(client, message)

   Handles an incoming quit event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.nick(client, message)

   Handles an incoming nick change event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.who(client, message)

   Handles an incoming who event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void 

.. js:function:: IRCHandler.names(client, message)

   Handles an incoming names event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.mode(client, message)

   Handles an incoming mode notify event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.mode_change(client, message)

   Handles an incoming mode change event

   :param object client: A valid client object
   :param object message: A valid message object


.. js:function:: IRCHandler.topic(client, message)

   Handles an incoming topic notify event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.topic_change(client, message)

   Handles an incoming topic change event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.privmsg(client, message)

   Handles an incoming privmsg event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.action(client, message)

   Handles an incoming action event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.notice(client, message)

   Handles an incoming notice event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.usermode(client, message)

   Handles an incoming usermode event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.ctcp_response(client, message)

   Handles an incoming ctcp_response event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.ctcp_request(client, message)

   Handles an incoming ctcp request event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void

.. js:function:: IRCHandler.unknown(client, message)

   Handles an incoming unknown event

   :param object client: A valid client object
   :param object message: A valid message object
   :returns: void