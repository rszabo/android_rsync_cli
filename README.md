# andevbackup

Use rsync to copy data from your Android powered device.

**Does not** require root privileges on your device or client system.

Based on the blog post http://ptspts.blogspot.se/2015/03/how-to-use-rsync-over-adb-on-android.html
and uses files from https://github.com/pts/rsyncbin/

## Usage

The script operates as follows:

  - Uses `adb` (Android Debug Bridge) to test if `rsync` is installed and configured.
  - Installs `rsync` and `rsyncd.conf` to /data/local/tmp/ on the device.
  - Executes `rsync` on the device as server and forwards a local port.
  - Executes a copy of the script with parameter `--copy` to start fetching new files.

### Example Output

```
user@host ~/.priv/backup/ $ andevbackup
Android Device Backup
---
MAIN: Connecting to device...
Configuring /tmp/rsyncd.conf
[100%] /sdcard/rsyncd.conf
Executing: adb forward tcp:6010 tcp:1873
MAIN: Starting local rsync in wait mode
MAIN: Starting remote rsync on your device
--copy: Waiting for rsync to respond...
Executing: rsync -av --size-only rsync://127.0.0.1:6010/root/ .
2017/01/26 22:08:57 [28493] connect from localhost (127.0.0.1)
receiving file list ...
Connecting to already running rsync server...
......done
./

sent 28 bytes  received 434435 bytes  57928.40 bytes/sec
total size is 28636481965  speedup is 65912.36
COPY: Completed with pid #87431.
MAIN: Killed main script with exit code #0
zsh: terminated  andevbackup

real    0m6.802s
user    0m0.046s
sys     0m0.101s
```

## Dependencies

  - `adb` (Android Debug Bridge, https://developer.android.com/studio/command-line/adb.html)
  - CLI tools: `rsync` `sed` `cat` `wget` `du`

### OS X/macOS

  - `brew` (https://brew.sh)

## Tests

Tested on stock Android 6.0, device Huawei Honour P8 running OS X El Capitan and Debian 8 64-bit.

## License

MIT

## About

andevbackup (Android Device Backup) developed by Richard K. Szabó to work on Linux and OS X/macOS
(`brew` required).

  - https://richardkszabo.me

Original solution by Péter Szabó (no relation or association):

  - https://github.com/pts
  - http://ptspts.blogspot.se/2015/03/how-to-use-rsync-over-adb-on-android.html

## Changelog

See `git log`.
