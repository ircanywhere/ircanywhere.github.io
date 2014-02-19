EventManager
============

*(c) 2013-2014 http://ircanywhere.com*

**Author:** Ricki Hastings

IRCAnywhere server/events.js
 
.. js:class:: EventManager.EventManager()

   Constructor, does nothing

   :returns: void

.. js:attribute:: EventManager.channelEvents

   A list of events relating to channels

.. js:function:: EventManager.this._insert(client, message, type[, user, force])

   Inserts an event into a backlog after all the checking has been done
   this api is private and EventManager.insertEvent should be used instead

   :param object client: A valid client object
   :param object message: A valid message object from `irc-message`
   :param string type: Event type
   :param object [user]: An optional user object
   :param boolean [force]: An optional force boolean to force the event into the '*' status window
   :returns: void

.. js:function:: EventManager.insertEvent(client, message, type)

   Inserts an event into the backlog, takes a client and message object and a type
   Usually 'privmsg' or 'join' etc.

   :param object client: A valid client object
   :param object message: A valid message object from `irc-message`
   :param string type: Event type
   :returns: void

.. js:function:: EventManager.determineHighlight(client, message, type, ours)

   Determine whether a message should be marked as a highlight or not for the specific
   IRC client. Currently this does not support anything other than looking at their nickname.

   :param object client: A valid client object
   :param object message: A valid message object from `irc-message`
   :param string type: Event type
   :param boolean ours: Whether this message comes from this client
   :returns: true or false

.. js:function:: EventManager.getPrefix(client, user)

   Gets the channel prefix for the irc client and the user object. A valid object returned is
   in the format of: ::
    
   {prefix: '+', sort: 5};

   :param object client: A valid client object
   :param object user: A valid user object
   :returns: A valid prefix object