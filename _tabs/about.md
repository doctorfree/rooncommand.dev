---
# the default layout is 'page'
icon: fas fa-info-circle
order: 7
---

> **"The cosmic operating system uses a command line interface. It runs on
> something like a teletype, with lots of noise and heat; punched-out bits
> flutter down into its hopper like drifting stars. The demiurge sits at his
> teletype, pounding out one command line after another, specifying the values
> of fundamental constants of physics:**
>
> `universe -G 6.672e-11 -e 1.602e-19 -h 6.626e-34 -protonmass 1.673e-27`
>
> **and when he’s finished typing out the command line, his right pinky hesitates
> above the enter key for an aeon or two, wondering what’s going to happen;
> then down it comes—and the whack you hear is another Big Bang."**
>
> ― Neal Stephenson, In the Beginning...Was the Command Line

<div align="center">
  <img src="https://raw.githubusercontent.com/wiki/doctorfree/RoonCommandLine/assets/rooncommandline.png" style="width:800px;height:140px;" alt="RoonCommandLine" />
</div>

## Overview

The Roon Command Line project provides Bash and Python scripts to enable
command line control of the Roon audio system over a local network.

**Note:** No modifications are made to the Roon Core. The RoonCommandLine
package resides entirely on other systems within your local area network.

Currently the command line Roon control scripts provide support for:

- Play album by album name
- Play artist name
- Play genre
- Play playlist by playlist name
- Play tag
- Play Roon Radio
- Play named album by specified artist
- Play named track by specified artist
- Play composer
- Play named album by specified composer
- Play named album in specified genre
- Play named artist in specified genre
- Issue one of the following commands in the specified zone
  - group
  - ungroup
  - play
  - play_all
  - pause
  - pause_all
  - playpause
  - stop
  - stop_all
  - next
  - previous
  - mute (toggle muted/unmuted in selected zone or zone grouping)
  - mute_all (toggle muted/unmuted in all zones)
  - shuffle (toggle shuffle/unshuffle zone playback)
  - repeat (toggle loop/unlooped zone playback)
- Get zone information and settings
- Get track/artist/album now playing in specified zone or all zones
- List albums, artists, albums by artist, tracks by artist, albums by composer, composers, albums by genre, artists by genre, genres, playlists, live radio stations, tags, and Roon zones
- Set the default Roon output zone
- Set the volume level in a specified Roon zone or zone grouping
- Select Roon audio zone or zone grouping
- Enable/disable track fade out and fade in

In addition, search capabilities have been added to the scripts
with partial matching facilities. Thus a substring can be supplied to use as a
search term with partial matching returning albums, artists, playlists, genres,
or tags which contain the specified substring (case sensitive). The special search
term `__all__` indicates match all albums, artists, playlists, genres, or tags.

All commands and playback can target a specified Roon output zone.

Additional detail and info can be found in the
[RoonCommandLine Wiki](https://github.com/doctorfree/RoonCommandLine/-/wikis/home).
