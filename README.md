
Logserver Patch for IoURT 4.1
=============================

INTRO
-----

This repository contains the IoUrbanTerror gameserver code, the scope of the project is to patch the code in such a manner that the logging is done via UDP rather than written to file.

This enables gameserver farms to have a single separate server for logging and game stats, and gamebot developers to avoid opening and parsing logfiles or installing the gamebot on the same machine used by the gameserver.

Kudos to Rambetter who set up a svn repository having many useful patches. The original code of this project was taken from his svn repo. You can find it here: http://forums.urbanterror.info/topic/18495-svn-repository-for-iourbanterror-exploit-fixes/


USAGE
-----

* download and build the code: the executable will be created inside the build/ folder.
* backup your ~/.q3a/q3ut4 folder.
* create default.cfg (touch ~/.q3a/q3ut4/default.cfg) otherwise the gameserver won't start.
* create autoexec.cfg and put in it:

	seta logserver_enable "1"
	seta logserver_address "localhost:27961"
	seta logserver_user "yourname"
	seta logserver_password "yourpass"

* use netcat to listen for incoming udp packets on the selected port (27961):

	nc -ul 27961

* start the server. Yopu should receive in netcat the string

	"\uyourname\pyourpass"

   repeated 10 times.

TODO
----

*The authentication part. The server now sends user and password plaintext via udp, it would be nice if there was some sort of encryption. The client has to reply with ok/fail messages.

*The protocol (message format).

*Find where the server sends the log.

*Write the log sending fcn.

*Write the logserver.


FUTURE DEVELOPMENT
------------------

Well, a kewl gamebot/logger/banbot system written in C and able to manage several gameservers at once.


LEARN IOQ3/IOURT
----------------

If you want some directions on how the ioquake3 server works, read this: http://nrfw.org/q3_coding_tips.html
It explains briefly:
-the big picture;
-how to add cvars;
-how to keep static data in the gameserver memory;
-how to send a message via UDP.

