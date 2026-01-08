# FreePBX Stereo Recording

```properties
; globals_custom.conf
MONITOR_REC_OPTION=Db
MIXMON_FORMAT=sln
MIXMON_POST=sox -t raw -r 8000 -e signed -b 16 -c 2 "^{MIXMONITOR_FILENAME}" "^{MIXMONITOR_FILENAME}.wav" && rm "^{MIXMONITOR_FILENAME}" && mv "^{MIXMONITOR_FILENAME}.wav" "^{MIXMONITOR_FILENAME}"
```

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/freepbx_globals_custom.dark.png">
  <source media="(prefers-color-scheme: light)" srcset="assets/freepbx_globals_custom.light.png">
  <img alt="preview" src="assets/freepbx_globals_custom.light.png">
</picture>

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
