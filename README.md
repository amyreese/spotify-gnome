Spotify Gnome Integration
-------------------------

This program provides Gnome media key support for the Spotify client on Linux.

The Spotify client supports DBus for controlling the player, using the
[MPRIS Specification](http://www.mpris.org/2.1/spec/), but does not listen for basic
media key signals provided by Gnome.  This program acts as a "wrapper" around Spotify
to translate media key signals from Gnome and send them to the Spotify client.

It supports the play/pause, stop, next, and previous signals, and is compatible with
both Gnome 2 and Gnome 3.


Installation
------------

Verify that your copy of Spotify installed its binary to `/usr/bin/spotify`:

    $ which spotify
	/usr/bin/spotify

If it was installed to a different location, you will need to edit `bin/spotify` to set
`spotify_bin` to the appropriate path.

Copy `bin/spotify` to `/usr/local/bin/spotify`, or a different path that takes precedent
over the location of your `spotify` binary:

    $ sudo install bin/python /usr/local/bin/

Launching `spotify` via application launcher or from the command line should now start
the wrapper first, which will then launch the real Spotify client.  Enjoy having media
keys that work for both Spotify and other media players.


License
-------

Spotify-Gnome was created by [John Reese](http://johnmreese.com), and copyright (c) 2011.

Spotify-Gnome is licensed under the MIT license.  See the LICENSE files for details.

