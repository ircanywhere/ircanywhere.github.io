IRCFactory
==========

*(c) 2013-2014 http://ircanywhere.com*

**Author:** Ricki Hastings

IRCAnywhere server/factory.js
 
.. js:class:: IRCFactory.IRCFactory()

   The IRCFactory object which handles communication with the irc-factory package
   This object is not hookable or extendable because plugins can deny the execution of
   functions when they hook into it, the results could be disasterous. If incoming events
   need to be hooked onto you could hook onto the IRCHandler object.
    
   The default `irc-factory` options are below: ::
    
       {
           events: 31920,
           rpc: 31930,
           automaticSetup: true
       }
    
   The `fork` setting comes from our configuration object and is inserted when `init` is ran.

   :returns: void

.. js:attribute:: IRCFactory.options

   The `irc-factory` options to use

   :type: object 

.. js:function:: IRCFactory.init()

   Initiates the irc factory and it's connection and sets up an event handler
   when the application is ready to run.

   :returns: void

.. js:function:: IRCFactory.handleEvent(event, object)

   Handles incoming factory events, events are expected to come in the following format: ::
    
       [ '52d3fc718132f8486dcde1d0', 'privmsg' ] { nickname: 'ricki-',
           username: 'ia1',
           hostname: '127.0.0.1',
           target: '#ircanywhere-test',
           message: '#ircanywhere-test WORD UP BROSEPTH',
           time: '2014-01-22T18:20:57.323Z',
    
   More advanced docs can be found at https://github.com/ircanywhere/irc-factory/wiki/Events

   :param array[string] event: A valid event array from irc-factory `['52d3fc718132f8486dcde1d0', 'privmsg']`
   :param object object: A valid event object from irc-factory
   :returns: void

.. js:function:: IRCFactory.create(network)

   Sends the command to `irc-factory` to create a new irc client with the given settings.
   If the client already exists it will be dropped by `irc-factory`.

   :param object network: A valid client object
   :returns: void

.. js:function:: IRCFactory.destroy(key)

   Sends the command to destroy a client with the given key. If the client doesn't exist
   the command will just be dropped.

   :param objectid key: A client key which has the type of a Mongo ObjectID
   :returns: void

.. js:function:: IRCFactory.send(key, command, args)

   Calls an RPC command on the irc-factory client, usually used to send
   commands such as /WHO etc. It's probably best to use CommandManager in most cases

   :param objectid key: A client key which has the type of a Mongo ObjectID
   :param string command: An IRC command to send, such as 'mode' or 'join'
   :param array args: An array of arguments to send delimited by a space.
   :returns: void