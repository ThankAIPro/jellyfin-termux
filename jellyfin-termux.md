# Install Jellyfin on Termux [In Proot]
This guide shows two methods of installing Jellyfin on termux

Note: only tested on aarch64/arm64

Note: I am not updating it anymore as you can install Jellyfin directly in termux now, just install `jellyfin-server` package in termux, tho you might have issues the jellyfin's ffmpeg if so then use `jellyfin --ffmpeg $(which ffmpeg)` to run jellyfin instead

These steps are same for both methods:

1. Update the repo
```
pkg update
```

2. Install proot-distro and ffmpeg (ffmpeg is only required in Method 2)
```
pkg install proot-distro ffmpeg -y
```

3. Install ubuntu and Login to it
```
proot-distro install ubuntu
proot-distro login ubuntu
```

4. Update and upgrade the packages in ubuntu
```
apt update && apt upgrade -y
```

5. .NET 7.0 [workaround](https://github.com/dotnet/runtime/issues/85556):
* Use nano (or editor of your choice) to make a file in `/etc/profile.d`
```
nano /etc/profile.d/02-dotnet-fix.sh
```
* Paste the following to set the value of `DOTNET_GCHeapHardLimit` to `1C0000000` (You might need to lower the value to get it to work):
```
export DOTNET_GCHeapHardLimit=1C0000000
```
* Save and exit nano by pressing `CTRL + x` then `y` then `enter`
* Make it executable
```
chmod +x /etc/profile.d/02-dotnet-fix.sh
```
* Logout and log back into proot

Method 1:

6. Install sudo curl and gnupg
```
apt install sudo curl gnupg -y
```

7. Follow the step 2 to 6 in the official ubuntu installation guide for Jellyfin [here](https://jellyfin.org/docs/general/installation/linux#ubuntu)
```
testando código
```

8. Create a symbolic link for Jellyfin web client (as it's in the wrong folder)
```
ln -s /usr/share/jellyfin/web /usr/lib/jellyfin/bin/jellyfin-web
```

9. Run Jellyfin
```
jellyfin
```
* Note: if you get network related errors add `--nonetchange` parameter to jellyfin

10. Give it a few minutes to finish startup then goto http://localhost:8096 to setup Jellyfin


Method 2:

6. Install necessary packages (skip wget if you have it installed in termux, also replace `74` with the latest version of libicu)
```
apt install wget libicu74 libfontconfig1 ca-certificates -y
```

7. Make a new folder in /opt by the name jellyfin and cd into it
```
mkdir /opt/jellyfin
cd /opt/jellyfin
```

8. Download the latest generic linux build for your architecture from [here](https://jellyfin.org/downloads/linux) with `wget` (make sure you download the correct architecture for you device)
```
wget https://repo.jellyfin.org/files/server/linux/latest-stable/arm64/jellyfin_10.10.6-arm64.tar.gz
```

9. Extract it with tar
```
tar xvzf jellyfin_10.10.6-arm64.tar.gz
```

10. Create four sub-directories for Jellyfin data
```
mkdir data cache config log
```
11. Use nano to make a script to run Jellyfin
```
nano jellyfin.sh
```
* Paste the following:
```
#!/bin/bash
JELLYFINDIR="/opt/jellyfin"

$JELLYFINDIR/jellyfin/jellyfin \
 -d $JELLYFINDIR/data \
 -C $JELLYFINDIR/cache \
 -c $JELLYFINDIR/config \
 -l $JELLYFINDIR/log \
 --ffmpeg /data/data/com.termux/files/usr/bin/ffmpeg
```
* Note: if you get network related errors add `--nonetchange` parameter to jellyfin in the `jellyfin.sh`
* Save and exit nano by pressing `CTRL + x` then `y` then `enter`

12. Make it executable 
```
chmod +x jellyfin.sh
```

13. Run it
```
/opt/jellyfin/jellyfin.sh
```

14. Give it a few minutes to finish startup then goto http://localhost:8096 to setup Jellyfin


Thanks to @vikoadi and @t-e-s-tweb for `DOTNET_GCHeapHardLimit=1C0000000` and `--nonetchange` fix
