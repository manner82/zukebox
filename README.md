==================================================================
zukebox: Juke Box
==================================================================

ZukeBox is a very simple "Juke Box" application for playing music from Youtube.

Project goals:
 - RESTful API for adding tracks, controlling the playback
 - The tracks are downloaded with youtube-dl and cached on disk
 - The playback is done with python-vlc
 - Browser extensions

It is in POC phase, use it own your own risk.
Currently no automated tests, many things are not configurable yet, the project is in early stage.

Developing
----------

    $ python bootstrap.py
    $ export PATH=$PWD/bin:$PATH
    $ buildout
    $ zukebox

Installation
------------

The easiest way to install most Python packages is via ``easy_install`` or ``pip``::

    $ easy_install zukebox

Installing as a systemd daemon
------------------------------

Starting automatically with systemd (you might need to modify username/path):

    $ cp -a etc/systemd/system/zukebox.service /etc/systemd/system/zukebox.service 
    $ chmod 664 /etc/systemd/system/zukebox.service
    $ systemctl daemon-reload
    $ systemctl start zukebox   # (optional) try if it works
    $ systemctl enable zukebox

ZukeBox is started with screen, so eg you can attach to it by:

    $ screen -r

(Make sure you are the same user you are running zukebox with.)

After this, pressing "Ctrl+a" "d" moves it back to the background.

Usage
-----

Start ``zukebox`` application and use the REST api.

Adding a track::

    $ http POST 0.0.0.0:5000/player/tracks url="https://www.youtube.com/watch?v=lWqeHVOQa58" user="Tomi"

Getting the tracks::

    $ http GET 0.0.0.0:5000/player/tracks

Remove a track::

    $ http DELETE 0.0.0.0:5000/player/tracks/0

Getting the recent tracks::

    $ http GET 0.0.0.0:5000/player/recent-tracks

Control the player::

    $ http PATCH 0.0.0.0:5000/player/control time:=240 # seek
    $ http PATCH 0.0.0.0:5000/player/control playing:=false # play/pause
    $ http PATCH 0.0.0.0:5000/player/control volume:=50 # change volume

Copyright & License
-------------------

  * Copyright 2015, Tamas Domok
  * License: MIT
