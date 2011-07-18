Spotify Gnome Integration
-------------------------

This program provides Gnome media key support for the
[Spotify Linux client](http://www.spotify.com/us/download/previews/).

The Spotify client supports DBus for controlling the player, using the
[MPRIS Specification](http://www.mpris.org/2.1/spec/), but does not listen for basic
media key signals provided by Gnome.  This program acts as a "wrapper" around Spotify
to translate media key signals from Gnome and send them to the Spotify client.

It supports the play/pause, stop, next, and previous signals, and is compatible with
both Gnome 2 and Gnome 3.

Many thanks to [Mike Houston at kothar.net](http://kothar.net/index.php/blog/30-spotifydbus)
and [Fran Diéguez at Mabishu](http://www.mabishu.com/blog/2010/11/15/playing-with-d-bus-interface-of-spotify-for-linux/)
for their blog postings that pointed me in the right directions to get this implemented.


Installation
------------

Verify that your copy of Spotify installed its binary to `/usr/bin/spotify`:

    $ which spotify
	/usr/bin/spotify

If it was installed to a different location, you will need to edit `bin/spotify` to set
`spotify_bin` to the appropriate path.

Copy `bin/spotify` to `/usr/local/bin/spotify`, or a different path that takes precedent
over the location of your `spotify` binary:

    $ sudo install bin/spotify /usr/local/bin/

Launching `spotify` via application launcher or from the command line should now start
the wrapper first, which will then launch the real Spotify client.  Enjoy having media
keys that work for both Spotify and other media players.


Support
-------

Spotify-Gnome was created by [John Reese](http://johnmreese.com), and copyright (c) 2011.
Spotify-Gnome is licensed under the MIT license.  See the LICENSE files for details.

Bugs can be reported on [my bug tracker](http://leetcode.net/mantis/).

