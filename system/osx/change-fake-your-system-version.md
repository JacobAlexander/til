# How to change (fake) your system version

**Fair warning:** once you set your system version to lower, various apps - including Preview, Safari, Mail, System Preferecnes and so on - may not run properly or even at all (this is why it's also a VERY GOOD IDEA to have iTerm 2 installed or any other termnal emulator other than the official Terminal.app - hey, just sayin') - change version back and you'll be saved.

If you are in need of faking your system version for few seconds (because gem isn't installing or app ain't running), you just have to edit one .plist file. Note that you must edit it as a superuser, so for example using Vim:

```
sudo vi /System/Library/CoreServices/SystemVersion.plist
```

Just remember to quit using `:wq!` as file is opened up in a read-only mode.

**Note:** it make take a reboot for some apps to notice the change.

Example of disguising as Maverick on Yosemite:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
  ...
  <key>ProductVersion</key>
  <!-- I need to be Maverick today! -->
  <!-- <string>10.10.2</string> -->
  <string>10.9</string>
</dict>
</plist>
```
