# Install Jellyfin on Termux [In Proot]
This guide shows two methods of installing Jellyfin on termux

Note: only tested on aarch64/arm64

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

Method 1:

5. Install sudo curl and gnupg
```
apt install sudo curl gnupg -y
```

6. Follow the step 3 to 6 in the official ubuntu installation guide for Jellyfin [here](https://jellyfin.org/docs/general/installation/linux#ubuntu)


7. Create a symbolic link for Jellyfin web client (as it's in the wrong folder)
```
ln -s /usr/share/jellyfin/web /usr/lib/jellyfin/bin/jellyfin-web
```
8. Run Jellyfin
```
jellyfin
```
9. Goto http://localhost:8096 to setup Jellyfin


Method 2:

5. Install necessary packages (skip wget if you have it installed in termux)
```
apt install wget libicu70 ca-certificates
```

6. Make a new folder in /opt by the name jellyfin and cd into it
```
mkdir /opt/jellyfin
cd /opt/jellyfin
```

7. Download the latest generic linux build for your architecture from [here](https://jellyfin.org/downloads/linux) with `wget` (make sure you down the correct architecture for you device)
```
wget https://repo.jellyfin.org/releases/server/linux/stable/combined/jellyfin_10.8.8_arm64.tar.gz
```

8. Extract it with tar
```
tar xvzf jellyfin_10.8.8_arm64.tar.gz
```

9. Create a symbolic link so you can easily upgrade
```
ln -s jellyfin_10.8.8 jellyfin
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
* Save and exit nano by pressing `CTRL + x` then `y` them `enter`

12. Make it executable 
```
chmod +x jellyfin.sh
```

13. Run it
```
/opt/jellyfin/jellyfin.sh
```

14. Goto http://localhost:8096 to setup Jellyfin
