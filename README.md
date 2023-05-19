# LogosLinux-winehqRollbackSteps
Documentation of steps used to rollback `winehq-staging` from `v8.8` to `v8.7`

## Issue encountered:
- Followed the steps to install `winehq-staging` which by default installed `v8.8`.
- There seems to be an issue with this version and the ability to index after a Logos installation.

Others reported no issues with `winehq-staging=8.7`
These are the steps and commands run to downgrade to `winehq-staging=8.7`

This was started after a complete purge of `.wine*` from the system, but tested with an install of `v8.8` and then completed the rollback.

## Updated Steps to Install Logos on Linux with `winehq-staging=8.7`

- Run the following commands to install Wine staging
- Skip to [START HERE](**START HERE if you already have `winehq-staging` installed**) if you already have everything installed

## Install `winehq-staging`

1. Install `winehq-staging` with default version

```
sudo dpkg --add-architecture i386
```

```
sudo mkdir -pm755 /etc/apt/keyrings
```

```
sudo wget -O /etc/apt/keyrings/winehq-archive.key https://dl.winehq.org/wine-builds/winehq.key
```

```
sudo wget -NP /etc/apt/sources.list.d/ https://dl.winehq.org/wine-builds/ubuntu/dists/jammy/winehq-jammy.sources
```

```
sudo apt install --install-recommends winehq-staging
```

---

## **START HERE if you already have `winehq-staging` installed**

### Steps to downgrade

1. Check with version of `winehq-staging` that you have

```
dpkg -s winehq-staging
```

Output from my machine:

```
Package: winehq-staging
Status: install ok installed
Priority: optional
Section: otherosfs
Installed-Size: 73
Maintainer: Rosanne DiMesio <dimesio@earthlink.net>, Marcus Meissner <meissner@suse.com>
Architecture: amd64
Source: wine-staging
Version: 8.8~jammy-1
Replaces: wine, wine-amd64, wine-i386, wine1.4, wine1.4-amd64, wine1.4-i386, wine1.5, wine1.5-amd64, wine1.5-i386, wine1.6, wine1.6-amd64, wine1.6-i386, wine1.7, wine1.7-amd64, wine1.7-i386, wine32, wine64
Provides: wine, wine-amd64, wine-i386, wine1.4, wine1.4-amd64, wine1.4-i386, wine1.5, wine1.5-amd64, wine1.5-i386, wine1.6, wine1.6-amd64, wine1.6-i386, wine1.7, wine1.7-amd64, wine1.7-i386, wine32, wine64
Depends: wine-staging (= 8.8~jammy-1)
Conflicts: wine, wine-amd64, wine-i386
Description: WINE Is Not An Emulator - runs MS Windows programs
 Wine is a program which allows running Microsoft Windows programs
 (including DOS, Windows 3.x and Win32 executables) on Unix.
```

2. Went ahead and cleaned out the cache

```
sudo apt-get clean
```

3. Install `aptitude`

```
sudo apt install aptitude
```

4. Get a list of the names of available packages

```
aptitude versions winehq-staging
```

5. From this list get the PACKAGE-NAME for the version that you want to rollback to.

**NOTE**: For my system, I used `8.7~jammy-1`

6. Install `v8.7` and all dependencies

```
sudo apt install --install-recommends winehq-staging=8.7~jammy-1 wine-staging=8.7~jammy-1 wine-staging-amd64=8.7~jammy-1 wine-staging-i386:i386=8.7~jammy-1
```

7. Re-check `winehq-staging` installed version which should reflect the PACKAGE-NAME from above.

```
dpkg -s winehq-staging
```

Output from my machine after the rollback:

```
Package: winehq-staging
Status: install ok installed
Priority: optional
Section: otherosfs
Installed-Size: 73
Maintainer: Rosanne DiMesio <dimesio@earthlink.net>, Marcus Meissner <meissner@suse.com>
Architecture: amd64
Source: wine-staging
Version: 8.7~jammy-1
Replaces: wine, wine-amd64, wine-i386, wine1.4, wine1.4-amd64, wine1.4-i386, wine1.5, wine1.5-amd64, wine1.5-i386, wine1.6, wine1.6-amd64, wine1.6-i386, wine1.7, wine1.7-amd64, wine1.7-i386, wine32, wine64
Provides: wine, wine-amd64, wine-i386, wine1.4, wine1.4-amd64, wine1.4-i386, wine1.5, wine1.5-amd64, wine1.5-i386, wine1.6, wine1.6-amd64, wine1.6-i386, wine1.7, wine1.7-amd64, wine1.7-i386, wine32, wine64
Depends: wine-staging (= 8.7~jammy-1)
Conflicts: wine, wine-amd64, wine-i386
Description: WINE Is Not An Emulator - runs MS Windows programs
 Wine is a program which allows running Microsoft Windows programs
 (including DOS, Windows 3.x and Win32 executables) on Unix.
```

8. Lock/hold updates to `winehq-staging` to keep it pinned to `v8.7`

```
sudo apt-mark hold winehq-staging
```

---

## Complete Download `LogosLinuxInstaller.sh`

1. Install shell script dependencies

```
sudo apt install dialog
```

```
sudo apt install patch lsof wget sed grep gawk winbind cabextract x11-apps bc libxml2-utils curl
```

2. Download the LogosLinuxInstaller script from the following link:

```
https://github.com/ferion11/LogosLinuxInstaller/releases/download/v3.7.1/LogosLinuxInstaller.sh
```

3. Locate directory where `LogosLinuxInstaller.sh` was downloaded

4. Make `LogosLinuxInstaller.sh` shell script executable

```
chmod +x LogosLinuxInstaller.sh
```

5. Run shell script for installation and follow terminal prompts

```
./LogosLinuxInstaller.sh
```

## **Notes:**
- I was able to subsequently install Logos using the `LogosLinuxInstall.sh` script.
- I did not have Logos installed previously, so I am not sure if this ends up requiring a Logos reinstall or not.
- I have not yet had time to run the indexing for my initial install.
- Please let me know if there are any issues/problems with this sequence and I will adjust.

## Thank you!
