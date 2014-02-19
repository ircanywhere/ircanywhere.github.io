ChannelManager
==============

*(c) 2013-2014 http://ircanywhere.com*

**Author:** Ricki Hastings

IRCAnywhere server/channels.js
 
.. js:class:: ChannelManager.ChannelManager()

   This object is responsible for managing everything related to channel records, such as
   the handling of joins/parts/mode changes/topic changes and such.
   As always these functions are extendable and can be prevented or extended by using hooks.

   :returns: void

.. js:function:: ChannelManager.getChannel(network, channel)

   Gets a tab record from the parameters passed in, strictly speaking this doesn't have to
   be a channel, a normal query window will also be returned. However this class doesn't
   need to work with anything other than channels.
    
   A new object is created but not inserted into the database if the channel doesn't exist.

   :param string network: A network string such as 'freenode'
   :param string channel: The name of a channel **with** the hash key '#ircanywhere'
   :returns: A channel object straight out of the database.

.. js:function:: ChannelManager.insertUsers(key, network, channel, users[, force])

   Inserts a user or an array of users into a channel record matching the network key
   network name and channel name, with the option to force an overwrite

   :param objectid key: A valid Mongo ObjectID for the networks collection
   :param string network: The network name, such as 'freenode'
   :param string channel: The channel name '#ircanywhere'
   :param array[object] users: An array of valid user objects usually from a who/join output
   :param boolean [force]: Optional boolean whether to overwrite the contents of the channelUsers
   :returns: The final array of the users inserted

.. js:function:: ChannelManager.removeUsers(network[, channel, users])

   Removes a specific user from a channel, if users is omitted, channel should be equal to a nickname
   and that nickname will be removed from all channels records on that network.

   :param string network: A valid network name
   :param string [channel]: A valid channel name
   :param array users: An array of users to remove from the network `or` channel
   :returns: void

.. js:function:: ChannelManager.updateUsers(key, network, users, values)

   Updates a user or an array of users from the specific channel with the values passed in.

   :param objectid key: A valid Mongo ObjectID for the networks collection
   :param string network: The name of the network
   :param array users: A valid users array
   :param object values: A hash of keys and values to be replaced in the users array
   :returns: void

.. js:function:: ChannelManager.updateModes(key, capab, network, channel, mode)

   Takes a mode string, parses it and handles any updates to any records relating to
   the specific channel. This handles user updates and such, it shouldn't really be called
   externally, however can be pre and post hooked like all other functions in this object.

   :param objectid key: A valid Mongo ObjectID for the networks collection
   :param object capab: A valid capabilities object from the 'registered' event
   :param string network: Network name
   :param string channel: Channel name
   :param string mode: Mode string
   :returns: void

.. js:function:: ChannelManager.updateTopic(key, channel, topic, setby)

   Updates the specific channel's topic and setby in the internal records.

   :param objectid key: A valid Mongo ObjectID for the networks collection
   :param string channel: A valid channel name
   :param string topic: The new topic
   :param string setby: A setter string, usually in the format of 'nickname!username@hostname'
   :returns: void