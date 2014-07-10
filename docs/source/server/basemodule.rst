Module
======

*(c) 2013-2014 http://ircanywhere.com*

**Author:** Ricki Hastings

IRCAnywhere server/basemodule.js
 
.. js:class:: Module.Module()

   Base class for creating modules

   :returns: void.. js:class:: Module.undefined()



.. js:function:: Module.extend(object)

   Extend function used to extend objects with base module functionality so they
   can hook into core events. This should only be called once per module, if a module
   needs to contain multiple files, this object can be pulled in from multiple files
   with exports and require and the output can be extended once.

   :param object object: The module object to extend
   :returns: void.. js:class:: Module.undefined()



.. js:function:: Module.bindFunction(key, classObject, split, fn, object)

   Used to bind hooks for a function on a core object

   :param string key: Class name
   :param object classObject: Class object
   :param array split: An array containing two values, 'pre|post|hook' and method name
   :param function fn: A callback
   :param object object: The base object where the fn belongs in
   :returns: void