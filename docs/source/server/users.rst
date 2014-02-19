UserManager
===========

*(c) 2013-2014 http://ircanywhere.com*

**Author:** Ricki Hastings

IRCAnywhere server/users.js
 
.. js:class:: UserManager.UserManager()

   Responsible for handling user related actions ie registering, logging in, forgot passwords etc.
   Most of these actions are triggered via API calls.

   :returns: void

.. js:function:: UserManager.init()

   Sets up the API routes and anything else needed by the user manager class.
   Such as timers and the SMTP connection

   :returns: void

.. js:function:: UserManager.timeOutInactive()

   Responsible for disconnecting any inactive users
    
   This function is ran every hour or so, but not perfectly precise, but it shouldn't
   drift off too much because it re-corrects it self.

   :returns: void

.. js:function:: UserManager.isAuthenticated(data)

   Checks the sent in authentication string (should be "token=actualToken")
   all in string format, this is how it is sent in the authentication command and
   how it lies as a cookie. It also takes a full cookie string, such as
   "someKey=1; someOtherKey=2; token=actualToken" and the token will only be parsed and used.
    
   Returns a valid user object which can be used to set on the socket for example or
   HTTP request, returns false if invalid

   :param object data: A valid data object from sock.js


.. js:function:: UserManager.registerUser(req, res)

   Handles user registrations, it takes req and res objects from express at the moment
   however it should probably stay this way, because the api to register a user is at /api/register.
   I can't see a reason to change this to take individual parameters.

   :param object req: A valid request object from express
   :param object res: A valid response object from express
   :returns: An output object for the API call

.. js:function:: UserManager.userLogin(req, res)

   Handles the login call to /api/login and sets an appropriate cookie if successful.

   :param object req: A valid request object from express
   :param object res: A valid response object from express
   :returns: An output object for the API call

.. js:function:: UserManager.userLogout(req, res)

   Handles the call to /api/logout which is self explanatory.

   :param object req: A valid request object from express
   :param object res: A valid response object from express
   :returns: An output object for the API call

.. js:function:: UserManager.forgotPassword(req, res)

   Handles the call to /api/forgot to send a forgot password link

   :param object req: A valid request object from express
   :param object res: A valid response object from express
   :returns: An output object for the API call

.. js:function:: UserManager.resetPassword(req, res)

   Handles the call to /api/reset which will be called when the reset password link is visited
   Checking is done to make sure a token exists in a user record.

   :param object req: A valid request object from express
   :param object res: A valid response object from express
   :returns: An output object for the API call

.. js:function:: UserManager.updateSettings(req, res)

   Handles the call to /api/settings/updatesettings which will update the settings for that user
   checking for authentication and validating if necessary.

   :param object req: A valid request object from express
   :param object res: A valid response object from express
   :returns: An output object for the API call

.. js:function:: UserManager.resetPassword(req, res)

   Handles the call to /api/settings/changepassword which is almost identical to resetPassword
   however it checks for authentication and then changes the password using that user, it doesn't
   take a token though.

   :param object req: A valid request object from express
   :param object res: A valid response object from express
   :returns: An output object for the API call

.. js:function:: UserManager.updatePassword(user, password, confirmPassword[, currentPassword])

   Updates a users password, doesn't bypass any checkings, just doesn't
   define how you select the user, so via a token or direct user object

   :param object user: A valid user object from `isAuthenticated`
   :param string password: The new password to set
   :param string confirmPassword: The same password again
   :param string [currentPassword]: The current password
   :returns: An output object for the API call

.. js:function:: UserManager.onUserLogin(me[, force])

   An event which is called when a successful login occurs, this logic is kept out of
   the handler for /api/login because it's specific to a different section of the application
   which is the networkManager and ircFactory.

   :param object me: A valid user object
   :param boolean [force]: Whether to force the reconnect of a disconnected client
   :returns: void

.. js:function:: UserManager.parse(file, replace)

   Looks for a template and parses the {{tags}} into the values in replace
   and returns a string, used to parse emails. Very basic parsing which will
   probably be replaced by something more powerful in the future with HTML outputs.

   :param string file: The name of the email template
   :param object replace: A hash of keys and values to replace in the template
   :returns: A parsed email template