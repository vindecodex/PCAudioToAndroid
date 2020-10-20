# PCAudioToAndroid
Stream Audio from PC to Android (Ubuntu)

## Instructions

Clone and cd inside the project

1. Find you source_name.

```bash
pactl list | grep "Monitor Source"
```

2. Open `shareAudio` with editor and replate `<source_name_here>` with you source name.

```bash
#!/bin/sh
case "$1" in
  start)
    $0 stop 
    pactl load-module module-simple-protocol-tcp rate=48000 format=s16le channels=2 source=<source_name_here> record=true port=8000
    ;;
  stop)
    pactl unload-module `pactl list | grep tcp -B1 | grep M | sed 's/[^0-9]//g'`
    ;;
  *)
    echo "Usage: $0 start|stop" >&2
    ;;
esac
```
3. Run below command.

```bash
./pashare start
netstat -nlt | grep 8000 
telnet 127.0.0.1 8000
```

4. Install and connect to your computer ip

[Download PulseDroid APK](https://github.com/dront78/PulseDroid/tree/master/bin)

or

[Download Simple Protocol Player](https://play.google.com/store/apps/details?id=com.kaytat.simpleprotocolplayer)


## Source
[StackOverflow](https://superuser.com/questions/605445/how-to-stream-my-gnu-linux-audio-output-to-android-devices-over-wi-fi)
