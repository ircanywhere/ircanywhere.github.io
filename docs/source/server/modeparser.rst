ModeParser
==========

*(c) 2013-2014 http://ircanywhere.com*

**Author:** Ricki Hastings

IRCAnywhere server/modeparser.js
 
.. js:class:: ModeParser.ModeParser()

   Responsible for parsing mode strings into unstandable actions
   and also responsible for applying those actions to a channel/user object.
   
   None of these functions can be hooked onto or extended seen as though it's just not
   needed and could be malicious if people are altering mode string, bugs relating to this
   are difficult to find, if you want to hook a mode change hook to IRCHandler.mode_change()

   :returns: void

.. js:function:: ModeParser.sortModes(capabilities, modes)

   Sorts a mode string into an object of instructions that we can use to perform actions
   based on what the mode string suggests, ie apply operator to 'someone', or set +m on the channel

   :param object capabilities: A valid capabilities object from a client
   :param string modes: A mode string `+no-v rickibalboa Gnasher`
   :returns: A valid modeArray object

.. js:function:: ModeParser.changeModes(capabilities, modes, modeArray)

   Handles the object of instructions returned from sortModes, and applies them

   :param object capabilities: A valid capabilities object from a client
   :param object modes: The current mode string for the channel (not including all parameters)
   :param object modeArray: A valid modeArray object from `sortModes()`
   :returns: The channel mode string with the changes applied.

.. js:function:: ModeParser.handleParams(capabilities, users, modeArray)

   Applies any mode changes that contain status related modes, usually qaohv modes
   minus: rickibalboa: -o > will remove the o flag from the nickname record
   minus: rickibalboa: +v > will set the v flag on the nickname record

   :param object capabilities: A valid capabilities object from a client
   :param object users: A valid users array for a channel
   :param object modeArray: A valid modeArray from `sortModes`
   :returns: An array of users that have been affected by the mode change