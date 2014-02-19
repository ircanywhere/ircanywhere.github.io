Installing IRCAnywhere
======================

Installing
~~~~~~~~~~

Once the environment is setup properly you can proceed with installing **IRCAnywhere**.

The first step is to clone the github repo, or you can install from the ``0.2-alpha`` release. However a number of stability changes have been made since then so the ``development`` branch is usually the most stable. ::

    $ git clone https://github.com/ircanywhere/ircanywhere.git
    $ git checkout development
    $ cd ircanywhere

**or** from `0.2-alpha` ::

    $ wget https://github.com/ircanywhere/ircanywhere/archive/v0.2-alpha.tar.gz
    $ tar xvf v0.2-alpha.tar.gz
    $ cd ircanywhere-0.2-alpha

Then we need to install the dependencies (I've no idea how this runs on windows, I'm not expecting it to run well because we use fibers. I'd recommend unix/linux based operating systems).

``$ npm install``

Next you'll need to build the client source, you'll need to make sure ``grunt-cli`` is installed via npm. Once that is done you can run these commands. You can set grunt up to watch files if you're doing any development work (including writing plugins) by running `grunt watch` after the following commands. ::

    $ npm install -g grunt-cli
    $ grunt

Finally, edit the configuration file ``config.example.json`` a few things will need changed by default, the ip address and port, and you'll need to include a smtp url if you want to be able to send emails out (forgot password links wont work without emails). Your MongoDB settings should be fine if you've followed these instructions. Finally rename it to ``config.json``.

Running
~~~~~~~

There are multiple ways you can run **IRCAnywhere**, you probably want to run it detaching from the console so it runs as a daemon, you can do that with the following commands:

``$ npm start``

**or**

``$ node . start``

Note that the above commands wont restart it's self when an exception occurs. To do this you're going to want to respond to signals to reboot if the system crashes or gets killed for some other reason. Traditionally node applications are ran with ``forever``, however there is a strange case causing ``irc-factory`` to reboot when the parent restarts which loses our ability to detach from IRC connections keeping them online between restarts, this is not good.

I use a program called `https://github.com/visionmedia/mon`_ to keep the process running. You should use ``node . run`` and not ``node . start`` when using ``mon`` because it will go into a restart loop if you don't.

``$ mon -d "node . run" -p ircanywhere.pid -l logs/mon.log``

If you're running in a production environment it would be better to run this behind a nginx proxy or similar. In the future there will be instructions on how to do this and the possibility to serve the css/js files via nginx. I'll also be implementing a way to sticky session via nginx when the system is clustered.

.. _https://github.com/visionmedia/mon: https://github.com/visionmedia/mon