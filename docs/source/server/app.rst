Application
===========

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

.. js:attribute:: Application.verbose

   A flag to determine whether verbose logging is enabled or not

   :type: boolean 

.. js:attribute:: Application.config

   A copy of the parsed config object

   :type: object 

.. js:attribute:: Application.packagejson

   A copy of the project's package.json object

   :type: object 

.. js:function:: Application.init()

   This is the main entry point for the application, it should NOT be called under any circumstances.
   However it can safely be extended by hooking onto the front or back of it using pre and post hooks.
   Treat this method like the main() function in a C application.

   :returns: void

.. js:function:: Application.setupOplog()

   This method initiates the oplog tailing query which will look for any incoming changes on the database.
   Incoming changes are then handled and sent to the global event emitter where other classes and modules
   can listen to for inserts, updates and deletes to a collection to do what they wish with the changes.

   :returns: void

.. js:function:: Application.setupWinston()

   This function sets up our winston logging levels and transports. You can safely extend
   or override this function and re-run it to re-initiate the winston loggers if you want to
   change the transport to send to loggly or something via a plugin.

   :returns: void

.. js:function:: Application.setupNode()

   Checks for a node record to store in the file system and database
   This is done to generate a 'unique' but always the same ID to identify
   the system so we can make way for clustering in the future.

   :returns: void

.. js:function:: Application.setupServer()

   This function is responsible for setting up the express webserver we use to serve the static files and
   the sock.js server which hooks onto it to handle the websockets. None of the routes or rpc callbacks
   are handled here.

   :returns: void