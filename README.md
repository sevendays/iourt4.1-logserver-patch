
Logserver Patch for IoURT 4.1
=============================

INTRO
-----

This repository contains the IoUrbanTerror gameserver code, the scope of the project is to patch the code in such a manner that the logging is done via UDP rather than written to file.

This enables gameserver farms to have a single separate server for logging and game stats, and gamebot developers to avoid opening and parsing logfiles or installing the gamebot on the same machine used by the gameserver.

Kudos to Rambetter who set up a svn repository having many useful patches. The original code of this project was taken from his svn repo. You can find it [in the UrbanTerror forums](http://forums.urbanterror.info/topic/18495-svn-repository-for-iourbanterror-exploit-fixes/ "post by rambetter on urt forum").


USAGE
-----

* download and build the code: the executable will be created inside the build/ folder.
* backup your ~/.q3a/q3ut4 folder.
* create default.cfg (touch ~/.q3a/q3ut4/default.cfg) otherwise the gameserver won't start.
* create autoexec.cfg and put in it:
<code>
    seta logserver_enable "1"
    seta logserver_address "localhost:27961"
    seta logserver_user "yourname"
    seta logserver_password "yourpass"
</code>
* use netcat to listen for incoming udp packets on the selected port (27961):
<code>
    nc -ul 27961
</code>
* start the server. You should read in netcat the string
<code>
    "\uyourname\pyourpass"
</code>
   repeated 10 times.

TODO
----

1. The authentication part. The server now sends user and password plaintext via udp, it would be nice if there was some sort of encryption. The client has to reply with ok/fail messages.

2. The protocol (message format).

3. Find where the server sends the log.

4. Write the log sending fcn.

5. Write the logserver.


FUTURE DEVELOPMENT
------------------

Well, a kewl gamebot/logger/banbot system written in C and able to manage several gameservers at once.


LEARN IOQ3/IOURT
----------------

If you want some directions on how the ioquake3 server works, read my [q3/urt coding tips](http://nrfw.org/q3_coding_tips.html "page on my website").

It explains briefly:

* the big picture;
* how to add cvars;
* how to keep static data in the gameserver memory;
* how to send a message via UDP.

