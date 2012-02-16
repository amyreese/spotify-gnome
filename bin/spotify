#!/usr/bin/env python2

import dbus
import dbus.service
from dbus.mainloop.glib import DBusGMainLoop
import gobject
import os
import subprocess
import time

spotify_bin = "/usr/bin/spotify"

class SpotifyPlayer(dbus.service.Object):
    def __init__(self, conn, object_path="/org/mpris/MediaPlayer2"):
        dbus.service.Object.__init__(self, conn, object_path)

class SpotifyGnome(object):

    def __init__(self):
        pid = os.fork()

        if pid == 0:
            time.sleep(1)
            print "Launching Spotify..."
            self.spotify = None
            args = [spotify_bin]
            os.execv(spotify_bin, args)

        else:
            print "Setting up DBus..."
            bus_loop = DBusGMainLoop(set_as_default=True)
            self.session_bus = dbus.SessionBus(mainloop=bus_loop)

            print "Connecting to NameOwnerChanged..."
            bus = self.session_bus.get_object("org.freedesktop.DBus",
                                              "/org/freedesktop/DBus")
            bus.connect_to_signal("NameOwnerChanged",
                                  self.name_owner_changed,
                                  arg0="org.mpris.MediaPlayer2.spotify")

            print "Connect to MediaKeys..."
            bus = self.session_bus.get_object("org.gnome.SettingsDaemon",
                                              "/org/gnome/SettingsDaemon/MediaKeys")
            bus.connect_to_signal("MediaPlayerKeyPressed",
                                  self.key_pressed)
            self.mediakeys = dbus.Interface(bus,
                                            "org.gnome.SettingsDaemon.MediaKeys")

            self.loop = gobject.MainLoop()
            self.loop.run()

            print "Done"

    def name_owner_changed(self, name, before, after):
        print "Received NameOwnerChanged:"
        print "  {0} - {1} - {2}".format(name, before, after)

        if name == "org.mpris.MediaPlayer2.spotify":
            if after:
                self.spotify_id = after
                self.spotify_bus = self.session_bus.get_object("org.mpris.MediaPlayer2.spotify",
                                                               "/org/mpris/MediaPlayer2")
                self.spotify = dbus.Interface(self.spotify_bus,
                                              "org.mpris.MediaPlayer2.Player")
                self.mediakeys.GrabMediaPlayerKeys("Spotify", time.time())
            else:
                self.mediakeys.ReleaseMediaPlayerKeys("Spotify")
                self.loop.quit()

    def key_pressed(self, *keys):
        print "Received MediaPlayerKeyPressed:"
        print "  " + repr(keys)

        if self.spotify:
            for key in keys:
                if key == "":
                    pass

                elif key == "Play":
                    self.spotify.PlayPause()

                elif key == "Stop":
                    self.spotify.Stop()

                elif key == "Next":
                    self.spotify.Next()

                elif key == "Previous":
                    self.spotify.Previous()

if __name__ == "__main__":
    SpotifyGnome()
