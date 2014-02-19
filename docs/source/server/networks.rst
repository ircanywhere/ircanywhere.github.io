NetworkManager
==============

*(c) 2013-2014 http://ircanywhere.com*

**Author:** Ricki Hastings

IRCAnywhere server/networks.js
 
.. js:class:: NetworkManager.NetworkManager()

   Responsible for handling everything related to networks, such as tracking changes
   removing, creating, changing tabs, creating and deleting networks etc.

   :returns: void

.. js:attribute:: NetworkManager.flags

   An object containing the valid network statuses

   :type: object 

.. js:function:: NetworkManager.init()

   Called when the application is ready to proceed, this sets up event listeners
   for changes on networks and tabs collections and updates the Client object with the changes
   to essentially keep the object in sync with the collection so we can do fast lookups, but
   writes to the collection will propogate through and update Clients

   :returns: void

.. js:function:: NetworkManager.getClients()

   Gets a list of networks, used by IRCFactory on synchronise
   to determine who to connect on startup, doesn't ever really need to be called
   also can be modified with hooks to return more information if needed.

   :returns: An object containing the clients that should be started up

.. js:function:: NetworkManager.addNetworkApi(req, res)

   Handles the add network api call, basically handling authentication
   validating the parameters and input, and on success passes the information
   to `addNetwork()` which handles everything else

   :param object req: A valid request object from express
   :param object res: A valid response object from express
   :returns: An output object for the API call

.. js:function:: NetworkManager.addNetwork(user, network, status)

   Adds a network using the settings specified to the user's set of networks
   This just adds it to the database and doesn't attempt to start it up.

   :param object user: A valid user object from the `users` collection
   :param object network: A valid network object to insert
   :param string status: A valid network status
   :returns: The network inserted or null if not

.. js:function:: NetworkManager.addTab(client, target, type[, select, active])

   Adds a tab to the client's (network unique to user) tabs, this can be a
   channel or a username.

   :param object client: A valid client object
   :param string target: The name of the tab being created
   :param string type: The type of the tab either 'query', 'channel' or 'network'
   :param boolean [select]: Whether to mark the tab as selected or not, defaults to false
   :param boolean [active]: Whether to mark the tab as active or not, defaults to true
   :returns: void

.. js:function:: NetworkManager.activeTab(client[, target, activate])

   Changes a tabs activity (not selection) - for example when you're kicked from a channel the tab
   wont be removed it will be just set to active: false so when you see it in the interface it will appear as
   (#ircanywhere) instead of #ircanywhere
   We can omit target and call activeTab(client, false) to set them all to false (such as on disconnect)

   :param object client: A valid client object
   :param string [target]: The name of the tab being altered, discard to mark all as active or inactive.
   :param boolean activate: Whether to set the tab as active or not
   :returns: void

.. js:function:: NetworkManager.removeTab(client, target])

   Removes the specified tab, be careful because this doesn't re-select one, you're expected to look
   for a removed tab, if it's the currently selected one, go back to a different one.

   :param object client: A valid client object
   :param string [target]: The name of the tab being altered, discard to remove all.
   :returns: void

.. js:function:: NetworkManager.connectNetwork(network)

   Connect the specified network record, should only really be called when creating
   a new network as IRCFactory will load the client up on startup and then determine
   whether to connect the network itself based on the options.
    
   However, it's also called when it appears that there is no connected client on the
   /reconnect command (and any other similar commands). We can determine this (sloppy)
   from checking client.internal.status. If in the case that it does exist, it doesn't
   matter if this is called really because irc-factory will prevent a re-write if the
   key is the same. We could consider looking at the response from factory synchronize
   but it might not yield a good result because of newly created clients since startup.

   :param object network: A valid network or client object
   :returns: void

.. js:function:: NetworkManager.changeStatus(query, status)

   Update the status for a specific network specified by a MongoDB query. The reason for
   this and not a straight ID is so we can do certain things such as checking if a network
   is marked as 'disconnected' during the `closed` event to determine whether to keep it as
   'disconnected' or mark it as 'closed'. So we can do much more elaborate queries here than
   just ID checking

   :param object query: A MongoDB query to select a network
   :param boolean status: A valid network status
   :returns: void