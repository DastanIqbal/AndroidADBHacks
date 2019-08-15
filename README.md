## AndroidADBHacks
### Copy text in clipboard
```
adb shell input text "<input text >"
```
### Send Media Scan Broadcast

```
adb shell am broadcast -a android.intent.action.MEDIA_MOUNTED -d file:///sdcard
```
The MEDIA_MOUNTED intent is no longer permitted (post KitKat) for non-system apps; try this instead.

It’s not recursive, though, and has to be run on the exact_file_name, so it’s not a good replacement.
```
adb shell am broadcast -a android.intent.action.MEDIA_SCANNER_SCAN_FILE -d file:///<file path>
```

If you need to rescan recursively, you can use this command (fix paths accordingly):
```
adb shell "find </file path/> -exec am broadcast -a android.intent.action.MEDIA_SCANNER_SCAN_FILE -d file://{} \\;"
````

Or like this (if above won't work for you):
```
adb shell "find <file path> | while read f; do am broadcast -a android.intent.action.MEDIA_SCANNER_SCAN_FILE -d \"file://${f}\"; done"

```
