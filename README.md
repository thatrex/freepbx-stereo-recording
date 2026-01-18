# FreePBX Stereo Recording

###### _Tested on FreePBX 17.0.24 (Asterisk 20.17.0 & 21.12.0)_

This [config](#config) allows FreePBX to record in stereo. FreePBX's CDR always plays recordings in mono, as such you will only hear the recording in stereo when downloaded.

This is great when it works, unfortunately it often doesn't, and I am yet to figure out why...

## Issue

Calls frequently fail to record as expected. While the failed recordings are in stereo and the correct speed, the pitch is too low and paired with frequent popping. [I found a post on the Asterisk forum where someone seemly has the same issue](https://community.asterisk.org/t/mixmonitor-quality-audio-issue-with-d-flag/), unfortunately without resolution.

This has nothing to do with the SoX processing. You can comment out `MIXMON_POST` and open the raw recordings in an audio editor with the following raw data format settings:

> **Format:** PCM Linear [16 bits (Little Endian / Intel)]  
> **Sample Rate:** 8000 Hz  
> **Channels:** 2 (stereo)

Any help regarding this issue is much appreciated.

## Instructions

1. Navigate to **Admin > Config Edit**.
2. Locate the file, `globals_custom.conf`.
3. Copy paste the [config](#config) into the file.
4. Save & apply config.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/freepbx_globals_custom.dark.png">
  <source media="(prefers-color-scheme: light)" srcset="assets/freepbx_globals_custom.light.png">
  <img alt="preview" src="assets/freepbx_globals_custom.light.png">
</picture>

## Config

```properties
MONITOR_REC_OPTION=Db
MIXMON_FORMAT=sln
MIXMON_POST=sox -t raw -r 8000 -e signed -b 16 -c 2 "^{MIXMONITOR_FILENAME}" "^{MIXMONITOR_FILENAME}.wav" && rm "^{MIXMONITOR_FILENAME}" && mv "^{MIXMONITOR_FILENAME}.wav" "^{MIXMONITOR_FILENAME}"
```

<!--
```properties
MONITOR_REC_OPTION=D ; D = Stereo Recording (also overwrites the default 'b')
MIXMON_FORMAT=sln
; The following converts the stereo RAW to a stereo WAV, then changes the file extension to sln.
; This allows recordings to be downloaded as stereo WAV while playback continues to work (in mono.)
MIXMON_POST=sox -t raw -r 8000 -e signed -b 16 -c 2 "^{MIXMONITOR_FILENAME}" "^{MIXMONITOR_FILENAME}.wav" && rm "^{MIXMONITOR_FILENAME}" && mv "^{MIXMONITOR_FILENAME}.wav" "^{MIXMONITOR_FILENAME}"
; The following converts the stereo RAW to a stereo OGG, then changes the file extension to sln.
; Both CDR playback and download works, however the downloaded file extension need to be manually changed to OGG.
;MIXMON_POST=sox -t raw -r 8000 -e signed -b 16 -c 2 "^{MIXMONITOR_FILENAME}" -C 10 "^{MIXMONITOR_FILENAME}.ogg" && rm "^{MIXMONITOR_FILENAME}" && mv "^{MIXMONITOR_FILENAME}.ogg" "^{MIXMONITOR_FILENAME}"
```
-->
