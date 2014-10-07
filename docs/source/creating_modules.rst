Using the module system
=======================

There are two ways to integrate your own code into IRCAnywhere, you can hook into the backend and frontend and choose to combine them in your modules.

Modules are located in the ``modules/`` folder and loaded automatically on startup, they require a specific directory structure to be loaded automatically. This guide will teach you how to create a basic hello world style module. For example, a module with server side code will have the following structure. ::

    modules
    `-- helloworld
        `-- server
            `-- index.js

Index.js will be the main entry point for the module, you can have other files and npm modules and require them into index.js if you need to.

Client side modules have the following directory structure. ::

    modules
    `-- helloworld
        `-- client
            `-- js
                `-- helloworld.js
            `-- less
            `-- templates

This code will be compiled into the javascript, css and templates if specified.

Server Side
~~~~~~~~~~~

Server side modules work by extending the `baseModule` object, each core component can be modified, extended, or have new functionality bound. Here is an example of how to bind a new command. ::

    /* hello world example module */
    baseModule.extend({
        commandManager: {
            'bind:helloworld': function (user, client, target, params) {
                console.log('hello world, you can use the arguments of this function to interact with the client object');
                console.log(arguments);
            }
        }
    });

Here we are extending the ``commandManager`` object, and telling the module manager to bind a new function named ``helloworld``, this will automatically be picked up by the command manager and the command will be accessible via ``/mycommand param1 param2``.

We can choose to override existing core functionality by using this method aswell, an example would be overriding the initialising function of any core component by doing ``bind:init`` **this should be done with caution**. We can use hooks to perform actions at specific intervals aswell by using ``pre``, ``post`` and ``hook`` instead of ``bind``. For example ::

    ircHandler: {
        'pre:closed': function (next, client, message) {
            console.log('do something before ircHandler.closed() is called');

            next();
            // call closed
        }
    }

This will call this function before ``ircHnalder.closed()`` is executed, allowing us to extend core functionality easily.

Client Side
~~~~~~~~~~~

Client side modules are compiled into the final javascript build, and can modify any of the frontend's functionality in a similar way to how the backend works. Because of how Ember works functionally, there isn't really a huge need for an API, we can just build our own controllers, views, templates exactly how they are built in the core frontend code.

In this example below you can see how a client side implementation of the ``/helloworld`` command can be created. ::

    App.InputController.reopen({
        commands: {
            '/helloworld': function() {
                console.log('hello world');
                console.log(arguments);
            }
        },
    });

We can use Ember's ``reopen`` to reopen any class and override existing core functionality. The client side javascript is currently undocumented and the module system is still partially complete, this section will be updated in the future.