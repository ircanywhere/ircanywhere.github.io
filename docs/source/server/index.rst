IRCAnywhere Daemon
==================

*(c) 2013-2014 http://ircanywhere.com*

**Author:** Ricki Hastings

IRCAnywhere server/app.js
 
.. js:class:: Application.Application()

   The applications's main object, contains all the startup functions.
   All of the objects contained in this prototype are extendable by standard
   rules.
    
   Examples: ::
    
       application.post('init', function(next) {
           console.log('do something after init() is run');
           next();
       });

   :returns: void

.. js:attr:: Application.verbose

   A flag to determine whether verbose logging is enabled or not

   :type: boolean 

.. js:attr:: Application.config

   A copy of the parsed config object

   :type: object 

.. js:attr:: Application.packagejson

   A copy of the project's package.json object

   :type: object 

.. js:func:: Application.init()

   This is the main entry point for the application, it should NOT be called under any circumstances.
   However it can safely be extended by hooking onto the front or back of it using pre and post hooks.
   Treat this method like the main() function in a C application.

   :returns: void

.. js:func:: Application.setupOplog()

   Sets up the oplog tracker

   :returns: void

.. js:func:: Application.setupWinston()

   Sets up the winston loggers

   :returns: void

.. js:func:: Application.setupNode()

   Checks for a node record to store in the file system and database
   This is done to generate a 'unique' but always the same ID to identify
   the system so we can make way for clustering in the future

   :returns: void

.. js:func:: Application.setupServer()

   Sets up the express and sockjs server to handle all HTTP / WebSocket requests

   :returns: void