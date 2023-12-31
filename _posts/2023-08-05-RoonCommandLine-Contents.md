---
title: RoonCommandLine Contents
author: doctorfree
date: 2023-08-05 12:55:00 +0800
tags: [info, commands, contents]
pin: true
img_path: "/posts/20230805"
---

A brief description of the [Commands](#commands),
[Python API scripts](#python-api-scripts), and
[Configuration files](#configuration-files) contained in the
[RoonCommandLine project](https://github.com/doctorfree/RoonCommandLine){:target="_blank"}{:rel="noopener noreferrer"}
along with links to each.

## Commands

- [**/usr/local/bin/roon**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/roon){:target="_blank"}{:rel="noopener noreferrer"}
  Shell script frontend that provides the primary user interface to communicate commands via the Python Roon API. Recommended usage is to issue Roon commands and queries via the `roon` frontend rather than executing the following commands directly.
- [**/usr/local/bin/clone_pyroon**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/clone_pyroon){:target="_blank"}{:rel="noopener noreferrer"} - Shell script to retrieve the pyroon project source code from Github and apply my patches
- [**/usr/local/bin/get_core_ip**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/get_core_ip){:target="_blank"}{:rel="noopener noreferrer"} - Shell script to retrieve the Roon Core IP address
- [**/usr/local/bin/get_zone_info**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/get_zone_info){:target="_blank"}{:rel="noopener noreferrer"} - Returns zones, their groupings, and their grouping compatibilities
- [**/usr/local/bin/get_zones**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/get_zones){:target="_blank"}{:rel="noopener noreferrer"} - Returns comma separated list of zones
- [**/usr/local/bin/play_album**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/play_album){:target="_blank"}{:rel="noopener noreferrer"} - Shell script frontend for playing a specified album in my Roon library
- [**/usr/local/bin/play_artist**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/play_artist){:target="_blank"}{:rel="noopener noreferrer"} - Shell script frontend for playing a specified artist in my Roon library
- [**/usr/local/bin/play_artist_album**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/play_artist_album){:target="_blank"}{:rel="noopener noreferrer"} - Shell script frontend for playing a specified album by artist in my Roon library
- [**/usr/local/bin/play_artist_track**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/play_artist_track){:target="_blank"}{:rel="noopener noreferrer"} - Shell script frontend for playing a specified track by artist in my Roon library
- [**/usr/local/bin/play_composer**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/play_composer){:target="_blank"}{:rel="noopener noreferrer"} - Shell script frontend for playing a specified compoer in my Roon library
- [**/usr/local/bin/play_composer_album**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/play_composer_album){:target="_blank"}{:rel="noopener noreferrer"} - Shell script frontend for playing a specified album by composer in my Roon library
- [**/usr/local/bin/play_genre_album**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/play_genre_album){:target="_blank"}{:rel="noopener noreferrer"} - Shell script frontend for playing a specified album in genre in my Roon library
- [**/usr/local/bin/play_genre_artist**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/play_genre_artist){:target="_blank"}{:rel="noopener noreferrer"} - Shell script frontend for playing a specified artist in genre in my Roon library
- [**/usr/local/bin/play_genre**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/play_genre){:target="_blank"}{:rel="noopener noreferrer"} - Shell script frontend to play a specified genre
- [**/usr/local/bin/play_playlist**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/play_playlist){:target="_blank"}{:rel="noopener noreferrer"} - Shell script frontend to play a specified playlist
- [**/usr/local/bin/play_radio**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/play_radio){:target="_blank"}{:rel="noopener noreferrer"} - Shell script frontend for playing Live Radio in a Roon zone
- [**/usr/local/bin/play_tag**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/play_tag){:target="_blank"}{:rel="noopener noreferrer"} - Shell script frontend to play a specified tag
- [**/usr/local/bin/list_albums**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/list_albums){:target="_blank"}{:rel="noopener noreferrer"} - Search and list the available Albums in your Roon Library
- [**/usr/local/bin/list_artists**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/list_artists){:target="_blank"}{:rel="noopener noreferrer"} - Search and list the available Artists in your Roon Library
- [**/usr/local/bin/list_artist_albums**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/list_artist_albums){:target="_blank"}{:rel="noopener noreferrer"} - Search and list the available Albums by Artist in your Roon Library
- [**/usr/local/bin/list_artist_tracks**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/list_artist_tracks){:target="_blank"}{:rel="noopener noreferrer"} - Search and list the available Tracks by Artist in your Roon Library
- [**/usr/local/bin/list_composer_albums**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/list_composer_albums){:target="_blank"}{:rel="noopener noreferrer"} - Search and list the available Albums by a Composer in your Roon Library
- [**/usr/local/bin/list_composers**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/list_composers){:target="_blank"}{:rel="noopener noreferrer"} - Search and list the available Composers in your Roon Library
- [**/usr/local/bin/list_genre_albums**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/list_genre_albums){:target="_blank"}{:rel="noopener noreferrer"} - Search and list the available Albums in a genre in your Roon Library
- [**/usr/local/bin/list_genre_artists**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/list_genre_artists){:target="_blank"}{:rel="noopener noreferrer"} - Search and list the available Artists in a genre in your Roon Library
- [**/usr/local/bin/list_genres**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/list_genres){:target="_blank"}{:rel="noopener noreferrer"} - Search and list the available Genres in your Roon Library
- [**/usr/local/bin/list_playlists**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/list_playlists){:target="_blank"}{:rel="noopener noreferrer"} - Search and list the available Roon Playlists
- [**/usr/local/bin/list_radio**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/list_radio){:target="_blank"}{:rel="noopener noreferrer"} - Search and list the available Roon Live Radio channels
- [**/usr/local/bin/list_tags**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/list_tags){:target="_blank"}{:rel="noopener noreferrer"} - Search and list the available Roon Library tags
- [**/usr/local/bin/list_zones**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/list_zones){:target="_blank"}{:rel="noopener noreferrer"} - List the available Roon Zones
- [**/usr/local/bin/set_volume**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/set_volume){:target="_blank"}{:rel="noopener noreferrer"} - Set the volume level of a Roon Zone
- [**/usr/local/bin/set_zone**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/set_zone){:target="_blank"}{:rel="noopener noreferrer"} - Set the Roon Zone in which subsequent commands will run
- [**/usr/local/bin/set_zone_group**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/set_zone_group){:target="_blank"}{:rel="noopener noreferrer"} - Set one of the Roon Zone groupings specified in roon_api.ini
- [**/usr/local/bin/zone_command**](https://github.com/doctorfree/RoonCommandLine/blob/master/bin/zone_command){:target="_blank"}{:rel="noopener noreferrer"} - Shell script frontend for commands to be issued in the selected Roon Zone (e.g. play, pause, mute, unmute, next track, previous track)

## Python API scripts

- [**/usr/local/Roon/api/**](https://github.com/doctorfree/RoonCommandLine/blob/master/api/README.md){:target="_blank"}{:rel="noopener noreferrer"} - Python scripts to call the Roon API with appropriate arguments
- [**/usr/local/Roon/api/get_core_ip.py**](https://github.com/doctorfree/RoonCommandLine/blob/master/api/get_core_ip.py){:target="_blank"}{:rel="noopener noreferrer"} - Python script to discover the Roon Core and retrieve its IP address
- [**/usr/local/Roon/api/list_albums.py**](https://github.com/doctorfree/RoonCommandLine/blob/master/api/list_albums.py){:target="_blank"}{:rel="noopener noreferrer"} - Python script to list albums in the Roon Library
- [**/usr/local/Roon/api/list_artists.py**](https://github.com/doctorfree/RoonCommandLine/blob/master/api/list_artists.py){:target="_blank"}{:rel="noopener noreferrer"} - Python script to list artists in the Roon Library
- [**/usr/local/Roon/api/list_genres.py**](https://github.com/doctorfree/RoonCommandLine/blob/master/api/list_genres.py){:target="_blank"}{:rel="noopener noreferrer"} - Python script to list genres in the Roon Library
- [**/usr/local/Roon/api/list_playlists.py**](https://github.com/doctorfree/RoonCommandLine/blob/master/api/list_playlists.py){:target="_blank"}{:rel="noopener noreferrer"} - Python script to list playlists in the Roon Library
- [**/usr/local/Roon/api/list_radio.py**](https://github.com/doctorfree/RoonCommandLine/blob/master/api/list_radio.py){:target="_blank"}{:rel="noopener noreferrer"} - Python script to list Live Radio channels in the Roon Library
- [**/usr/local/Roon/api/list_tags.py**](https://github.com/doctorfree/RoonCommandLine/blob/master/api/list_tags.py){:target="_blank"}{:rel="noopener noreferrer"} - Python script to list tags in the Roon Library
- [**/usr/local/Roon/api/list_zones.py**](https://github.com/doctorfree/RoonCommandLine/blob/master/api/list_zones.py){:target="_blank"}{:rel="noopener noreferrer"} - Python script to list Roon zones
- [**/usr/local/Roon/api/play_album.py**](https://github.com/doctorfree/RoonCommandLine/blob/master/api/play_album.py){:target="_blank"}{:rel="noopener noreferrer"} - Python script to play specified album
- [**/usr/local/Roon/api/play_artist.py**](https://github.com/doctorfree/RoonCommandLine/blob/master/api/play_artist.py){:target="_blank"}{:rel="noopener noreferrer"} - Python script to play specified artist
- [**/usr/local/Roon/api/play_genre.py**](https://github.com/doctorfree/RoonCommandLine/blob/master/api/play_genre.py){:target="_blank"}{:rel="noopener noreferrer"} - Python script to play specified genre
- [**/usr/local/Roon/api/play_playlist.py**](https://github.com/doctorfree/RoonCommandLine/blob/master/api/play_playlist.py){:target="_blank"}{:rel="noopener noreferrer"} - Python script to play specified playlist
- [**/usr/local/Roon/api/play_radio.py**](https://github.com/doctorfree/RoonCommandLine/blob/master/api/play_radio.py){:target="_blank"}{:rel="noopener noreferrer"} - Python script to play Roon Live Radio
- [**/usr/local/Roon/api/play_tag.py**](https://github.com/doctorfree/RoonCommandLine/blob/master/api/play_tag.py){:target="_blank"}{:rel="noopener noreferrer"} - Python script to play specified tag
- [**/usr/local/Roon/api/zone_command.py**](https://github.com/doctorfree/RoonCommandLine/blob/master/api/zone_command.py){:target="_blank"}{:rel="noopener noreferrer"} - Python script to execute specified command in selected zone
- [**/usr/local/Roon/api/zone_group.py**](https://github.com/doctorfree/RoonCommandLine/blob/master/api/zone_group.py){:target="_blank"}{:rel="noopener noreferrer"} - Python script to group zones

## Configuration files

The `roon` command and the Python scripts it executes utilize two configuration files.

- [**/usr/local/Roon/etc/roon_api.ini**](https://github.com/doctorfree/RoonCommandLine/blob/master/etc/roon_api.ini){:target="_blank"}{:rel="noopener noreferrer"} - Python script initialization file
- **/usr/local/Roon/etc/pyroonconf** - Auto generated shell variables used by the RoonCommandLine commands

## License, copyright, installation scripts, patches, and usage

- [**LICENSE**](https://github.com/doctorfree/RoonCommandLine/blob/master/LICENSE){:target="_blank"}{:rel="noopener noreferrer"} - Apache License version 2.0
- [**NOTICE**](https://github.com/doctorfree/RoonCommandLine/blob/master/NOTICE){:target="_blank"}{:rel="noopener noreferrer"} - Copyright notice
- [**Install**](https://github.com/doctorfree/RoonCommandLine/blob/master/Install){:target="_blank"}{:rel="noopener noreferrer"} - Installation script for Linux systems, Debian format install
- [**Uninstall**](https://github.com/doctorfree/RoonCommandLine/blob/master/Uninstall){:target="_blank"}{:rel="noopener noreferrer"} - Removal script for Linux systems, Debian format uninstall
- [**macInstall**](https://github.com/doctorfree/RoonCommandLine/blob/master/macInstall){:target="_blank"}{:rel="noopener noreferrer"} - Installation script for Mac OS
- [**macUninstall**](https://github.com/doctorfree/RoonCommandLine/blob/master/macUninstall){:target="_blank"}{:rel="noopener noreferrer"} - Removal script for Mac OS
- [**usage.txt**](https://github.com/doctorfree/RoonCommandLine/blob/master/usage.txt){:target="_blank"}{:rel="noopener noreferrer"} - Frontend "roon" script usage documentation
- [**patches/**](https://github.com/doctorfree/RoonCommandLine/blob/master/patches/README.md){:target="_blank"}{:rel="noopener noreferrer"} - Patches to the Python Roon API to extend its capabilities
