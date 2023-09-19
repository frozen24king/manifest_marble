## 1. xiaomi-marble specific forks ##

[Repo](http://source.android.com/source/developing.html) is a tool provided by Google that
simplifies using [Git](http://git-scm.com/book) in the context of the Android source.

### 1.1 Installing dependencies and Repo ###

Several packages are needed in order to build
```
sudo apt install bc bison build-essential ccache curl flex g++-multilib gcc-multilib git git-lfs gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5 libncurses5-dev libsdl1.2-dev libssl-dev libwxgtk3.0-gtk3-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev
```

Install Repo tool

```bash
# Make a directory where Repo will be stored and add it to the path
$ mkdir ~/.bin
$ PATH=~/.bin:$PATH

# Download Repo itself
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/.bin/repo

# Make Repo executable
$ chmod a+x ~/.bin/repo
```
### 1.2 Remove these old Repo ###

This repository contains the manifest file for an Android project. Below are the `rm -rf` commands to remove specific old paths:

```bash
# Remove these old paths since we are now cloning them from the new LineageOS repository

# hardware/qcom-caf/sm8450/audio/agm
rm -rf hardware/qcom-caf/sm8450/audio/agm

# hardware/qcom-caf/sm8450/audio/pal
rm -rf hardware/qcom-caf/sm8450/audio/pal

# hardware/qcom-caf/sm8450/audio/primary-hal
rm -rf hardware/qcom-caf/sm8450/audio/primary-hal

# hardware/qcom-caf/sm8450/display
rm -rf hardware/qcom-caf/sm8450/display

# hardware/qcom-caf/sm8450/media
rm -rf hardware/qcom-caf/sm8450/media

# vendor/qcom/opensource/audio-hal/st-hal-ar
rm -rf vendor/qcom/opensource/audio-hal/st-hal-ar

# vendor/qcom/opensource/agm
rm -rf vendor/qcom/opensource/agm

# vendor/qcom/opensource/pal
rm -rf vendor/qcom/opensource/pal

# hardware/xiaomi
rm -rf hardware/xiaomi

# vendor/qcom/opensource/display
rm -rf vendor/qcom/opensource/display

# vendor/qcom/opensource/commonsys/display
rm -rf vendor/qcom/opensource/commonsys/display

# vendor/qcom/opensource/commonsys-intf/display
rm -rf vendor/qcom/opensource/commonsys-intf/display
```

### 1.3 Initializing Repo ###

```bash
# Create a directory for the source files
# You can name this directory however you want, just remember to replace
# WORKSPACE with your directory for the rest of this guide.
# This can be located anywhere (as long as the fs is case-sensitive)
$ mkdir WORKSPACE
$ cd WORKSPACE

# Install Repo in the created directory
$ repo init -u https://github.com/frozen24king/manifest_marble.git -b marble-13 --git-lfs
```

### 1.4 Downloading the source tree ###

This is what you will run each time you want to pull in upstream changes. Keep in mind that on your
first run, it is expected to take a while as it will download all the required Android source files
and their change histories.

```bash
# Let Repo take care of all the hard work
#
# The -j# option specifies the number of concurrent download threads to run.
# 8 threads is a good number for most internet connections.
# You may need to adjust this value if you have a particularly slow connection.
$ repo sync --no-tags --no-clone-bundle --current-branch -j8
```
