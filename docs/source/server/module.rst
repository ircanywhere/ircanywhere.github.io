ModuleManager
=============

*(c) 2013-2014 http://ircanywhere.com*

**Author:** Rodrigo Silveira

IRCAnywhere server/module.js
 
.. js:class:: ModuleManager.ModuleManager()

   Handles loading of modules.

   :returns: void

.. js:function:: ModuleManager.loadModule(moduleName)

   Loads a module by name. The name should be the name of the folder containing the module.

   :param string moduleName: Name of module to load.
   :returns: void

.. js:function:: ModuleManager.loadAllModules()

   Loads all modules.

   :returns: void

.. js:function:: ModuleManager.bindModule(module)

   Bind events and expose module to core functionality and vice versa

   :param object module: A valid module object returned from require()
   :returns: void