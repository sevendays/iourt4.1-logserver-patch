To apply a patch from this directory, perform the following command from
the base directory ioUrT-server-4.1:

  patch -N -p0 < ./extra-patches/filename.patch

The "-N" flag is important in order to resolve conflicts that a couple
of the patches have with one another.  In particular, ip2loc.patch and
playerdb.patch have some minor conflicts; these conflicts will be reported
by the patch command.  Regardless of these warnings the patches should
apply fine no matter which order you apply them in.

================
block1337.patch:
================

Introduces a new server cvar sv_block1337.  By default it is set to 0, which
makes the server behave exactly the same as without this patch.  When
sv_block1337 is set to a positive value such as 1, clients attempting to
connect that have a qport of 1337 will not be allowed to connect, and will
be given a message "This server is not for wussies".  A known cheat sets
the client qport to 1337.


===================
challengeping.patch
===================

Fixes calculation of challenge ping.  If a server is full and a client keeps
trying to reconnect, he won't get the "Server is for low pings only" message.


===================
checkuserinfo.patch
===================

Without this patch, it's possible to send userinfo strings with characters
such as ';' or '\r'.  For example, I've gotten ioquake3 to give me a name
containing a semicolon (even though the game code renames me to "badinfo").
To prevent any potential exploit which may not be discovered as of yet, I
would suggest applying this patch.  What this patch does is rigorously check
the userinfo string from each client to make sure that it's well-formed and
that it does not contain any abnormal characters.  To enable this check after
applying this patch, set the server cvar sv_checkUserinfo to any nonzero
positive value.  Any client connecting with an abnormal userinfo will not
be allowed to connect.  Any client changing their userinfo to something
that does not pass sanity checks will be immediately kicked.


====================
forceautojoin.patch:
====================

Introduces a new server cvar sv_forceAutojoin.  By default it is set to 0,
which makes the server behave exactly the same as without this patch.  When
sv_forceAutojoin is set to a positive value such as 1, client commands
"team red" and "team blue" will be translated to "team free".  The former two
commands are sent to the server when the client presses the UI buttons to
join the red or blue team, and "team free" is sent to the server when the
client presses the autojoin button.  So, in essence, this patch forces
players to autojoin.  A message "Forcing autojoin" will be printed to the
user who sent the "team red" or "team blue" command.

Independent of sv_forceAutojoin, this patch also translates the commands
"team r" and "team b" to "team red" and "team blue", respectively.  In the
case where sv_forceAutojoin is enabled, sending these commands allows a client
to bypass the autojoin feature.  Players more familiar with using the
console are thus able to bypass the sv_forceAutojoin feature, which is really
aimed at assisting noobs.


================
forcecvar.patch:
================

Introduces a new rcon command.  Use it like so:

  rcon forcecvar <client> <cvar-key> <cvar-val>

<client> can be a player name or a client number, or "allbots".  Examples:

  rcon forcecvar 12 name n00bsyb00bsy
  rcon forcecvar wTf|crown name TehNoobPwner
  rcon forcecvar allbots funred capgn,shades,ponygn
  rcon forcecvar allbots funblue capyw,shades,ponygd
  rcon forcecvar allbots racered 1
  rcon forcecvar allbots raceblue 1
  rcon forcecvar allbots cg_rgb "240 108 146"

You can also delete a cvar by omitting the last argument like so:

  rcon forcecvar Rambetter name ""
  rcon forcecvar Rambetter name


===========================
freebsd-prescott32bit.patch
===========================

For 32 bit FreeBSD systems; enables a compile optimization which produces
a binary that can only run on Prescott architectures (or newer).


===============
incognito.patch
===============

Introduces a new rcon command.  Use it like so:

  rcon incognito

This will place your client into stealth mode.  Everybody in the server will
temporarily think that you've disconnected, but in reality you will be in
spectators.

Introduces another new rcon command.  Use it like so:

  rcon sendclientcommand <client> <command>...

<client> can be a player name or a client number, or "all" or "allbots".
Example:

  rcon sendclientcommand Rambetter cp "Hi, this is some big text"


=============
ip2loc.patch:
=============

Enables messages that look like the following when players connect:

  Rambetter connected
      from SAN DIEGO, CALIFORNIA (UNITED STATES)

In addition, players will have the location stored in the new "location"
cvar in their userinfo string.

To have this patch run correctly, you have to point your game server to
a valid ip2loc server.  Information on the ip2loc server can be found here:
http://daffy.nerius.com/ip2loc/

Here is a sample of lines you'll want to add to your game server's server.cfg:

  set sv_ip2locEnable "1" // default 0, don't enable
  set sv_ip2locHost "localhost:10020" // host and port for the ip2loc service
  set sv_ip2locPassword "pa55w0rd" // password for the ip2loc service

This patch also defines a new connectionless packet handler for a command
"getlocations".  This command is similar to "getstatus" except that server
cvars are not returned, and player locations are added to the player listing.


==================
logcallvote.patch:
==================

Console logging for callvotes from players.  This is an example of what you'll
see in your console:

  Callvote from Ramb (client #0, 160.33.43.5): kick Longbeachbean


==================
logrconargs.patch:
==================

Introduces a new server cvar sv_logRconArgs.  By default it is set to 0,
which makes the server behave exactly the same as without this patch.  When
sv_logRconArgs is set to a positive value such as 1, the logging format
of successful and unsuccessful rcon attempts is changed (improved, I hope).
The new rcon logging will look like this:

  Bad rcon from 160.33.43.5
  Rcon from 160.33.43.5: kick Longbeachbean


==================
namesanitize.patch
==================

Introduces a new init server cvar sv_sanitizeNames.  When set to 1 (default 0),
modifies the player names in the ioquake3 server code to resemble the
sanitized names in the QVM server code.  The player userinfo strings are
affected.  For example, white space is stripped and colors are removed.
The empty name gets converted to "UnnamedPlayer".  Because this is a CVAR_INIT,
you need to enable it by adding "+set sv_sanitizeNames 1" to your ioq3ded
command.


=================
noauthorize.patch
=================

Disable some legacy Q3 authorize server logic such as packet handlers.


==============
nokevlar.patch
==============

Mostly for jump servers, introduces a new init server cvar sv_noKevlar.  By
default it is set to 0, which makes the server behave exactly the same as
without this patch.  When sv_noKevlar is set to a positive value such as 1,
kevlar will be removed from all players entering the game.  In addition, the
server will try to give players a medkit if it's possible to do so.  Because
this is a CVAR_INIT, you need to enable it by adding "+set sv_noKevlar 1" to
your ioq3ded command.


===============
playerdb.patch:
===============

Adds support for an external ban system and player database.  Full
documentation for this system:  http://daffy.nerius.com/bansystem/
In short, here are things you should add to your game server's server.cfg
file:

  set sv_requireValidGuid "1" // default 0, don't require well-formed cl_guid
  set sv_playerDBHost "localhost:10030" // host and port of player database
  set sv_playerDBPassword "s3cr3t" // password for player database
  set sv_playerDBUserInfo "1" // default 0, don't send userinfo to database
  set sv_playerDBBanIDs "cheaters,asshats" // banlists in use, default none
  set sv_permaBanBypass "pa55" // default none

The last cvar, sv_permaBanBypass, can be set to a non-empty string to allow
players who are banned to enter the server.  This is essentially a password
to bypass the ban system completely.  The client would use this command:

  setu permabanbypass "pa55"


====================
specchatglobal.patch
====================

Introduces sv_specChatGlobal.  When this is set to a positive value, all spec
chat will be broadcast to all players, not just spectators.  By default this
cvar is 0, which leaves the behavior of spec chat unchanged.


======================
userinfooverflow.patch
======================

Fixes an undetected possibility of client userinfo string overflow.
