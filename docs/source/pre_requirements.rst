Pre Requirements
================

IRCAnywhere requires a few tools to be installed before we can start installing the package. The following tools are required to proceed `if you have these installed you can skip to the next page`;

* nodejs
* npm
* MongoDB

Installing Node.js and Npm
~~~~~~~~~~~~~~~~~~~~~~~~~~

First we'll install nodejs and npm `we recommend latest stable versions as always`.

* **Fedora**

 ``$ sudo yum install nodejs npm -y``

* **Mac OSX**

 ``$ brew install node npm``

* **Debian/Ubuntu**

 Latest versions of nodejs include npm aswell. ::

    $ sudo add-apt-repository ppa:chris-lea/node.js
    $ apt-get update
    $ apt-get install nodejs

Installing MongoDB
~~~~~~~~~~~~~~~~~~

Next we'll install MongoDB and set it up correctly.

* **Fedora**

 ``$ yum install mongo-10gen mongo-10gen-server``

 You may need to create a `/etc/yum.repos.d/mongodb.repo` file and add the following to it.

 64-bit operating system. ::

    [mongodb]
    name=MongoDB Repository
    baseurl=http://downloads-distro.mongodb.org/repo/redhat/os/x86_64/
    gpgcheck=0
    enabled=1

 32-bit operating system (not recommended for production). ::

    [mongodb]
    name=MongoDB Repository
    baseurl=http://downloads-distro.mongodb.org/repo/redhat/os/i686/
    gpgcheck=0
    enabled=1

* **Mac OSX** ::

    $ brew update
    $ brew install mongodb

* **Debian/Ubuntu**

 ``$ apt-get install mongodb-10gen``

The next step is setting up MongoDB correctly so we can take advantage of the oplog tailing features, to do this we need to start MongoDB with a replica set. It's likely your package manager started MongoDB when they finished installing it, so we need to shut it down first, do this with the following commands. ::

    $ mongo
    > use admin;
    > db.shutdownServer();

**or**

``$ killall -12 mongod``

We now need to start mongodb with a single replica set for oplog tailing. Although a single mongo server wouldn't need to be a replica set usually, they allow it for testing purposes, if you're planning on running ircanywhere in a production environment with a good number of users I would recommend setting up an actual cluster of servers here_ (you'll hear more about clustering ircanywhere processes together soon).

If you are running MongoDB from a config file, which is usually located at ``/etc/mongodb.conf``. Then you can edit this file and include the following line at the bottom: ::

   replSet = rs0
   fork = true

You can then restart MongoDB using the config file with the following commands: ::

    $ mongod --config /etc/mongodb.conf
    $ mongo
    > rs.initiate()

If the file doesn't exist you can start MongoDB with the following options to initiate a replica set (although I would recommend having a config file to save you passing in these options every time you reboot. Although this is getting out of the scope of this guide). You may need to run it as sudo. ::

    $ mongod --logpath /var/log/mongodb.log --replSet rs0
    $ mongo

Once you've started the mongo instance sucessfully you can connect to it with the `mongo` command, once connected you should see this: ::

   MongoDB shell version: 2.4.9
   connecting to: test
   rs0:PRIMARY>

If you see the `:PRIMARY>` suffix then you've set the replica set up successfully. If you're still having trouble you can try following this more detailed guide at `http://meteorhacks.com/lets-scale-meteor.html`_.

.. _here: https://docs.google.com/document/d/1rJ1Hi6Q9oQXPRrROJkL9xO-CQR7Unk1mPN4SHtSiY08/edit#heading=h.wivau77ttb0a
.. _http://meteorhacks.com/lets-scale-meteor.html: http://meteorhacks.com/lets-scale-meteor.html