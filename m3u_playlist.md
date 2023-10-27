# M3U Playlist

## #EXTM3U
* `url-epg="http://path/to/epg/api/"` prefix for getting channel epg for exact channel
* `url-tvg="http://path/to/epg.xml.gz"` path to EPG teleguide for the whole playlist
* `url-logo="http://path/to/icons/root/"` root for all channel icons
* `catchup=".."` alias for catchup-type
* `catchup-type=".."` specifies that there are archives for channels
   - `default` only replace variables
   - `flussonic, flussonic-hls` flussonic (HLS)
   - `flussonic-ts, fs` flussonic (MPEG-TS)
   - `flussonic-dash` flussonic (MPEG-DASH)
   - `shift` - `?utc=startUnix&amp;lutc=nowUnix`
   - `archive` - `?archive=startUnix&amp;archive_end=toUnix`
   - `xc` xtream codes
   - `append` appending value specified in catchup-source attribute to the base channel url
   - `timeshift` - `timeshift=startUnix&timenow=nowUnix`
* `catchup-time="10800"` duration for archives being available
* `catchup-days="3"` duration for archives being available
* `catchup-source="..."` allows override path for archive playback
   - `{key}`, `${token}`  user-configured token
   - `${start}`, `{utc}` show start (unix time)
   - `${timestamp}`, `{current_utc}` current time (unix time)
   - `${end}`, `{utcend}` show end (unix time)
   - `${login}`, `${password}` user-configured login and password
   - `${duration}` show duration (seconds)
   - `${durmin}` show duration (minutes)
   - `${offset}` delta from current time to show start (seconds)
   - `${start-year},${start-mon},${start-day},${start-hour},${start-min},${start-sec}` show start date/time variables
   - `${end-year},${end-mon},${end-day},${end-hour},${end-min},${end-sec}` show end date/time variables
* `tvg-shift="0"` marker specifying that epg data should be shifted by several hours
* `cache="500"`
* `deinterlace="1"`
* `aspect-ratio="16:9"`
* `refresh="N"` period of time when the playlist should be reloaded
* `max-conn="1"` provider allows user opening more connections at the same time
* `billed-till="timestamp"` unix time when user account will expire
* `billed-msg="some text"` custom message regarding user account
* `vod_library=""` url to vod library

## #EXTINF:-1 tag1="value1",CH1
* `ch-number="27"` default shortcut for channel when using remote keys switching channel
* `parent-code="0000"` if set, marks a channel as restricted that should be hidden
* `ch-id=".."` channel id. used only with combination when url-epg or url-logo are set in playlist header
* `tvg-chno=".."` channel no
* `tvg-id="abc.yz"` channel id in epg teleguide that was linked in the playlist header
* `tvg-name="Original"` original channel name
* `tvg-logo="http://path/to/logo.jpg"` link to channel logo
* `tvg-rec="1"` marker that channel contains archives (0 - off, 1 - on)
* `group-id=""` category this channel
* `group-title="Movies"` category this channel belongs to
* `group-logo="http://url/to/image.png"` category icon
* `catchup*` all catchup settings for channel
* `type="playlist"`, `content-type="playlist"` allows to merge another playlist inside the current one
* `type="movie"`, `type="series"` that the channel listed is not a channel
* `adult="1"` marker that channel is adult
* `tvg-shift="-2"` marker specifying that epg data should be shifted by several hours
* `audio-track="2"` try to autoselect 2nd audio track
* `codec="auto"` can specify which codec to use when playing (auto, hard, exo1, system, soft_vlc, external)

## #EXTHTTP:{..http tags..}
* `#EXTHTTP:{"Authorization":"","Origin":"https://google.com","Referer":"https://google.com/","User-Agent":"Chrome"}`

## #EXTVLCOPT:parameter="value"
* `http-user-agent` User-Agent
* `http-referrer` HTTP referrer
* `network-caching`

## #KODIPROP:parameter=value
* `inputstreamaddon=inputstream.adaptive`
* `inputstream.adaptive.manifest_type=` dash/hls
* `inputstream.adaptive.license_type=` DRM type
   - `com.widevine.alpha` Widevine
   - `org.w3.clearkey` Clearkey
   - `com.microsoft.playready` PlayReady
* `inputstream.adaptive.license_key=` License key or URL depending on the DRM type
   - license url for playready/widevine content
   - `abc:def`, `{"abc":"def","klm":"opq"}` static key for clearkey content
* `inputstream.adaptive.license_data` base64 of default_kid
* `inputstream.adaptive.stream_headers` extra headers (referer=https://google.com&user-agent=https://google.com/)

## M3U file format sample
```
#EXTM3U url-tvg="https://google.com/epg.xml.gz" url-logo="https://google.com/" catchup="" catchup-days="" catchup-source="" tvg-shift="" cache="" deinterlace="" aspect-ratio="16:9" refresh="60" max-conn="1" billed-till="" billed-msg=""
#EXTINF:-1 tvg-chno="1" tvg-id="1" tvg-name="tv1" tvg-logo="https://google.com/logo.png" group_id="1" group-logo="https://google.com/logo2.png" group-title="tv",TV1
#KODIPROP:inputstreamaddon=inputstream.adaptive
#KODIPROP:inputstream.adaptive.manifest_type=dash
#KODIPROP:inputstream.adaptive.license_type=clearkey
#KODIPROP:inputstream.adaptive.license_key=abc:def
#KODIPROP:inputstream.adaptive.stream_headers=referer=https://google.com/&user-agent=Mozilla/5.0
#EXTHTTP:{"origin":"https://google.com"}
#EXTVLCOPT:http-user-agent=Mozilla/5.0
#EXTVLCOPT:http-referrer=https://google.com/
#EXTVLCOPT:network-caching=500
https://google.com/tv1.mpd|drmScheme=clearkey&drmLicense=abc:def&Referer=https://google.com/&User-agent=Mozilla/5.0
```

### Player
* [XtreamPlayer](https://play.google.com/store/apps/details?id=com.devcoder.iptvxtreamplayer)
* [Tivimate](https://play.google.com/store/apps/details?id=ar.tvplayer.tv)
* [Televizo](https://play.google.com/store/apps/details?id=com.ottplay.ottplay)
* [OTT Navigator](https://ott-nav.com/)
* [Kodi](https://play.google.com/store/apps/details?id=org.xbmc.kodi)
* [MX Player](https://play.google.com/store/apps/details?id=com.mxtech.videoplayer.ad)
* [VLC](https://play.google.com/store/apps/details?id=org.videolan.vlc)
* [GSE](https://play.google.com/store/apps/details?id=com.gsetech.smartiptv2)
* [IPTV Extreme Pro](https://play.google.com/store/apps/details?id=com.pecana.iptvextremepro)
* [IPTV Pro](https://play.google.com/store/apps/details?id=ru.iptvremote.android.iptv.pro)
