---
# the default layout is 'page'
icon: fas fa-user-circle
order: 4
---

## RoonCommandLine Usage

**Note:** The first time you execute the `roon` command you may have to enable
the Python Roon API extension by clicking "Settings" -> "Extensions" -> "Enable"
in a Roon Remote client window. On most systems this will not be necessary as
this was performed during initial installation.

The Python Roon API scripts must be installed on a system that is on the same
local network as the Roon Core. The `roon` shell script is the primary user
interface. It accepts a wide variety of arguments and sends a command to the
Python Roon API system which then communicates with the Roon Core.

If no arguments are provided to the `roon` command then an interactive dialog
is presented from which the user can select commands and queries.

Here is the current output of "roon -u" which displays a usage message.

```
Usage: roon -A album -a artist -C composer -f [on|onlog|off|status] -g genre -G zone_group -i
 -l [albums|artists|artalbums|arttracks|composers|comalbums|genres|genalbums|genartists|playlists|playtracks|tags|zones]
 -c [group|ungroup|play|play_all|pause|pause_all|stop|stop_all|next|previous|shuffle|repeat|mute|mute_all]
 -s search -p playlist -T track -t tag -z zone -L -S -r radio
 -X ex_album -x ex_artist [-EuU]
Where:
 -A album selects an album to play
 -a artist selects an artist to list/play
 -C composer selects a composer to play
 -g genre selects a genre to list/play
 -i displays zone information (combine with '-z zone' for extended
  info on a specified zone, otherwise display info on all zones)
 -f [on|onlog|off|status] enables/disables fading/logging in specified zone
  'on' enables fading, 'onlog' fading and logging, 'off' disables fading
  (combine with '-z zone' for 'fading' in that zone)
 -n displays 'now playing' information for zones actively playing
 -N displays 'now playing' information for all zones
  (combine with '-z zone' for 'now playing' in only that zone)
 -p playlist selects a playlist to play
 -G zone_group specifies a zone grouping specified in roon_api.ini
 -L setup roon to execute local commands rather than remote via SSH
 -S Set Roon defaults in roon_api.ini
 -l [albums|artists|artalbums|arttracks|composers|comalbums|genres|genalbums|genartists|playlists|playtracks|tags|zones]
  indicates list albums, artists, albums by artist, composers, albums by composers, genres, albums in genre, artists in genre, playlists, tags, or Roon zones
 -r radio selects a live radio stream to play
 -s search specifies a term to search for in the lists retrieved with -l
 -T track specifies a track to play
 -t tag selects an tag to play
 -z zone selects the Roon Zone in which to play
 -c [group|ungroup|play|play_all|pause|pause_all|playpause|stop|stop_all|next|previous|shuffle|repeat|mute|mute_all]
  issues the command in the selected zone
  'mute' toggles the zone's muted or unmuted state
  'mute_all' toggles all zones' muted or unmuted state
  'pause_all' pauses playback in all zones
  'play_all' begins playback in all zones
  'stop_all' stops playback in all zones and releases devices
  'shuffle' toggles the zone's shuffled or unshuffled setting
  'repeat' toggles the zone's looping or non-looping setting
 -v volume sets the volume level in the selected zone
  The volume argument has the format [g:][r:][s:]num
  Where 'g' indicates set volume for all zones in the group
  'r' specifies use relative method volume setting
  's' specifies use relative_step method volume setting
  'num' can be absolute, relative, and negative or positive
 -X ex_album specifies a string to exclude from album/genre names
 -x ex_artist specifies a string to exclude from artist/composer/playlist names
 -u displays a full usage message with examples
 -U displays a usage message without examples
 -E displays examples with no usage message
Combine '-a artist' and '-A album' to play an album by a specified artist
Combine '-a artist' and '-T track' to play a track by a specified artist
Combine '-a artist' or '-A album' with '-g genre' to play an artist or album in a specified genre

Special search term __all__ matches all entries
Special name default plays the default setting in roon_api.ini

Example invocations
 Play artist:
  roon -a "Deep Purple"
 Play album by artist:
  roon -a "Deep Purple" -A Burn
 Play track by artist:
  roon -a "Aretha Franklin" -T Think
 Play artist in specified zone:
  roon -a "Jethro Tull" -z "Mac Pro DAC"
 Play genre:
  roon -g Classical
 Play default live radio:
  roon -r default
 Play playlist:
  roon -p "Bowie Favs"
 Play next track:
  roon -c next
 Stop play in specified zone:
  roon -c stop -z Kitchen
 Mute/Unmute a specified zone:
  roon -c mute -z "Mac Pro DAC"
 Mute/Unmute all zones:
  roon -c mute_all
 List all playlists containing the string 'Best':
  roon -l playlists -s Best
 List albums by artist:
  roon -l artalbums -a "Deep Purple"
 List artists containing the string 'Will' in the 'Country' genre:
  roon -l genartists -a Will -g Country
 List albums containing the string 'Magic' in the 'Rock' genre:
  roon -l genalbums -A Magic -g Rock
 Play artist containing the string 'Willie' in the 'Country' genre:
  roon -a Willie -g Country
 Play album containing the string 'Magic' in the 'Rock' genre:
  roon -A Magic -g Rock
 Group the zones listed in roon_api.ini Group_foobar:
  roon -G foobar -c group
 Set the volume level to 50 in the currently active zone
  roon -v 50
 Decrease the volume level by 10 in the currently active zone
  roon -v r:-10
 Set the volume level to 40 in all zones grouped with the zone named 'Mac Pro DAC'
  roon -v g:40 -z 'Mac Pro DAC'
 Increase the volume level by 20 in all zones grouped with the zone named 'Mac Pro DAC'
  roon -v g:r:20 -z 'Mac Pro DAC'
 Get info on all Roon zones
  roon -i
 Get extended info on Roon zone named 'Mac Pro DAC'
  roon -i -z 'Mac Pro DAC'
 Get now playing info on all zones regardless of state
  roon -N
 Get now playing info on all zones actively playing
  roon -n
 Get now playing info on Roon zone named 'Mac Pro DAC'
  roon -n -z 'Mac Pro DAC'
 Enable volume fading in default Roon zone
  roon -f on
 Disable volume fading in default Roon zone
  roon -f off
 NOTE: Use quotes to specify media names which contain spaces.
 For example, to play the album 'Love Bomb':
  roon -A "Love Bomb"
```

When playing media from the command line it is possible to specify a substring
with which a partial match can be made. In order to play media, either the full
name of the desired media or enough of a substring to uniquely match should be
supplied. This applies to playing an album, artist, composer, genre, playlist,
or tag. For example, the command "roon -a Tull" would play media by artist
"Jethro Tull" unless there were multiple artist name matches to the substring
"Tull". All partial matching is case sensitive - "roon -a tull" would not
match "Jethro Tull".

If multiple matches are found, the first match in the list is played.
To narrow a search, exclusion filtering can be performed. Use the `-x string`
argument to specify an exclusion substring for artist, composer, and playlist
library searches. Use the `-X string` argument to specify an exclusion
substring for album and genre library searches.

In a large Roon library where multiple matches may be frequent and large,
one approach is to first list the media you wish to play and based on the
list of matches returned construct exclusion arguments that narrow the matches
to a list whose first element is the media you wish to play. For example:

`roon -l genalbums -g Classical -A Mozart`

might return the following:

Albums in Classical genre with Mozart in name :

Berliner Philharmoniker plays Mozart
Bruch: Violin Concerto No. 1, Op. 26 - Mozart: Violin Concerto No. 1, K. 207
Mozart: Concertos For Two Pianos K 242 & 365; Kozeluch: Four Hands Piano Concerto
Mozart - Great Recordings
Resonances (Mozart, Berg, Liszt, Bartok, Gluck)

If you tried to play media using these arguments then the first in the
list would be played - "Berliner Philharmoniker plays Mozart". But you
want to play the second one performed byy Bruch. This can be accomplished
either by modifying the album search term or by using an album exclusion filter:

`roon -l genalbums -g Classical -A Mozart -X Berliner`

would list the "Violin Concerto No. 1, Op. 26" by Mozart fist. Alternately,

`roon -l genalbums -g Classical -A "Mozart: Violin"`

would also list the concerto first. Another search route for this album
would be by searching albums by composer rather than albums by genre:

`roon -l comalbums -C Mozart -A "Violin Concerto"`

Listing/playing media in the Roon Library "Composers" category searches the
entire Roon database of available Composers rather than limiting the search
to the albums or artists etc in your library. This opens up a pretty wide
search field of composers and their works.

Finally, to play the media you have located using one of the listing techniques
described above, simply re-run the same command used to list the media only
remove the `-l <listingtype>` arguments. For example, if the listing command:

`roon -l genalbums -g Classical -A Mozart -X Berliner`

produced a search result to your liking and you now wish to play the first
entry in that returned list, remove the `-l genalbums` argument and re-run the command:

`roon -g Classical -A Mozart -X Berliner`

Any listing command can be turned into a play command in a similar manner.

### Introduction to Using the Command Line

The command line has a long and storied history in computing. Read some of that
history, learn how to open a command line terminal window on various systems,
how to get started using the command line, and see some examples of why the command
line interface is so powerful by reading the RoonCommandLine wiki article
[Introduction to Using the Command Line](https://github.com/doctorfree/RoonCommandLine/-/wikis/Introduction-to-Using-the-Command-Line).

This introduction to the command line includes an example of how to automate
playback of Roon playlists in specified Roon zones at designated times of day.

### Voice Activated Roon Control

RoonCommandLine can be used to provide a command line interface for the remote
execution of commands via SSH or other facilities such as Google Assistant.
In this way, voice control of Roon can be implemented on mobile devices or
other "smart" devices. Example implementations using Apple Siri and
Google Assistant are described in the following RoonCommandLine Wiki articles.

#### Roon Voice Commands with Siri

The RoonCommandLine Wiki article
["Roon Voice Commands with Siri"](https://github.com/doctorfree/RoonCommandLine/-/wikis/Roon-Voice-Commands-with-Siri)
describes in detail how to setup Roon voice commands using Apple Shortcuts
on an iOS device. This method utilizes Siri to recognize the voice commands
and run the Shortcut which uses SSH to execute the command.

#### Roon Voice Commands with Google Assistant

The RoonCommandLine Wiki article
["Roon Voice Commands with Google Assistant"](https://github.com/doctorfree/RoonCommandLine/-/wikis/Roon-Voice-Commands-with-GA)
describes in detail how to setup Roon voice commands using the
[MMM-GoogleAssistant](http://wiki.bugsounet.fr/en/MMM-GoogleAssistant)
and [MMM-Detector](http://wiki.bugsounet.fr/en/MMM-Detector)
modules on a [MagicMirror](https://magicmirror.builders/).
This method utilizes Google Assistant recipes to control Roon with voice commands.
