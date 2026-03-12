# Installing IPA Files on Jailbroken Apple TV via Terminal

## Overview

This guide explains how to install IPA files (like Browser.ipa) on a jailbroken Apple TV 4 running tvOS 12.1.2 using SSH terminal access and ldid for code signing.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Quick Fix: ldid Not Available](#quick-fix-ldid-not-available)
- [Method 1: Install IPA with ldid (Recommended)](#method-1-install-ipa-with-ldid-recommended)
- [Method 2: Install Using AppSync](#method-2-install-using-appsync)
- [Troubleshooting](#troubleshooting)
- [Common Issues](#common-issues)

---

## Quick Fix: ldid Not Available

If you're getting **"Unable to locate package ldid"** when trying to `apt-get install ldid`, use this quick fix:

```bash
# Download and install ldid manually
curl -L -O https://github.com/ProcursusTeam/ldid/releases/download/v2.1.5-procursus7/ldid_2.1.5-procursus7_iphoneos-arm.deb
dpkg -i ldid_2.1.5-procursus7_iphoneos-arm.deb

# Verify it works
ldid -V
```

If curl doesn't work, see the [ldid troubleshooting section](#ldid-not-found) for more methods.

---

## Prerequisites

Before you begin, ensure you have:

1. **Jailbroken Apple TV 4** running tvOS 12.1.2 (or compatible version)
2. **SSH access** to your Apple TV (see main guide for setup)
3. **IPA file** ready (e.g., Browser.ipa on your desktop)
4. **Computer on same network** as your Apple TV
5. **Basic terminal knowledge**

---

## Method 1: Install IPA with ldid (Recommended)

This method uses `ldid` to sign the IPA file before installation, which is the most reliable approach.

### Step 1: Install ldid on Apple TV

First, SSH into your Apple TV and install ldid:

```bash
# SSH into your Apple TV
ssh root@your-apple-tv-ip

# Update package lists first
apt-get update

# Try to install ldid from repositories
apt-get install ldid
```

**If you get "Unable to locate package ldid"**, ldid is not in your default repositories. See the [ldid installation alternatives](#ldid-not-found) below for manual installation methods.

**If you get SSL certificate errors**, see the [SSL troubleshooting section](#ssl-certificate-errors).

### Step 2: Transfer IPA File to Apple TV

From your computer (not the Apple TV), transfer the IPA file using SCP:

```bash
# Navigate to where your IPA file is located (e.g., Desktop)
cd ~/Desktop

# Transfer IPA to Apple TV
scp "Browser new.ipa" root@your-apple-tv-ip:/var/root/
```

**Note**: If your filename has spaces, make sure to use quotes around it.

Alternative methods to transfer:
- Use `curl` or `wget` if the IPA is hosted online
- Use a file manager app installed via Nito TV

### Step 3: Extract and Sign the IPA

SSH back into your Apple TV:

```bash
ssh root@your-apple-tv-ip

# Navigate to where you uploaded the IPA
cd /var/root/

# Create a temporary directory for extraction
mkdir -p /var/root/ipa_temp
cd /var/root/ipa_temp

# Extract the IPA (IPA files are just ZIP archives)
unzip "../Browser new.ipa"

# Navigate to the Payload directory
cd Payload

# Find the .app bundle name
ls -la
# You should see something like "Browser.app"

# Sign the app with ldid
ldid -S Browser.app/Browser

# Or sign all executables in the app
find Browser.app -type f -exec ldid -S {} \;
```

### Step 4: Install the App

```bash
# Create the Applications directory if it doesn't exist
mkdir -p /var/containers/Bundle/Application/

# Copy the app to Applications
cp -r Browser.app /Applications/

# Set proper permissions
chmod -R 755 /Applications/Browser.app
chown -R mobile:mobile /Applications/Browser.app

# Register the app with SpringBoard
uicache -a
```

### Step 5: Respring and Launch

```bash
# Respring to refresh the app list
killall -9 SpringBoard

# Or reboot the Apple TV
reboot
```

After the reboot, the app should appear on your Apple TV home screen.

---

## Method 2: Install Using AppSync

If you have AppSync Unified installed, you can install unsigned IPAs more easily.

### Step 1: Install AppSync Unified

```bash
ssh root@your-apple-tv-ip

# Add the repo (if not already added)
echo "deb https://cydia.akemi.ai/ ./" > /etc/apt/sources.list.d/akemi.list

# Update and install
apt-get update
apt-get install com.linusyang.appsyncu
```

### Step 2: Transfer and Install IPA

```bash
# From your computer, transfer the IPA
scp "Browser new.ipa" root@your-apple-tv-ip:/var/root/

# SSH into Apple TV
ssh root@your-apple-tv-ip

# Use appinst to install (if available)
appinst "/var/root/Browser new.ipa"

# Or manually extract and copy
unzip "Browser new.ipa" -d /tmp/app_install/
cp -r /tmp/app_install/Payload/*.app /Applications/
chmod -R 755 /Applications/*.app
uicache -a
killall -9 SpringBoard
```

---

## Troubleshooting

### SSL Certificate Errors

If you get SSL certificate errors during `apt-get update`:

```bash
# Edit sources to use HTTP instead of HTTPS
nano /etc/apt/sources.list.d/nito.list

# Change https:// to http:// for all repos
# Example:
# FROM: deb https://nitosoft.com/electra ./
# TO:   deb http://nitosoft.com/electra ./

# Save and exit (Ctrl+O, Enter, Ctrl+X)
apt-get update
```

See the main [CHECKRA1N_NITOTV_GUIDE.md](CHECKRA1N_NITOTV_GUIDE.md#ssl-certificate-errors-with-apt-get-or-wget) for more SSL troubleshooting.

### ldid Not Found

If ldid is not available via apt-get (error: "Unable to locate package ldid"), you need to install it manually. Here are multiple methods:

**Method 1: Download Pre-compiled ldid Binary (Easiest)**

```bash
# Download pre-compiled ldid for ARM
curl -L -O https://github.com/ProcursusTeam/ldid/releases/download/v2.1.5-procursus7/ldid_2.1.5-procursus7_iphoneos-arm.deb
dpkg -i ldid_2.1.5-procursus7_iphoneos-arm.deb

# Or if curl fails, try wget
wget https://github.com/ProcursusTeam/ldid/releases/download/v2.1.5-procursus7/ldid_2.1.5-procursus7_iphoneos-arm.deb
dpkg -i ldid_2.1.5-procursus7_iphoneos-arm.deb

# Verify installation
ldid -V
```

**Method 2: Use Saurik's Repository**

```bash
# Add Saurik's repository
echo "deb http://apt.saurik.com/ ./" > /etc/apt/sources.list.d/saurik.list

# Update and install
apt-get update
apt-get install ldid

# If SSL errors, use HTTP instead of HTTPS in the repository URL
```

**Method 3: Download Binary Directly**

```bash
# Download standalone ldid binary
curl -L -O https://github.com/ProcursusTeam/ldid/releases/latest/download/ldid
chmod +x ldid
mv ldid /usr/bin/ldid

# Or use a known working version
curl -L -O http://apt.saurik.com/debs/ldid_2.1.2-1_iphoneos-arm.deb
dpkg -i ldid_2.1.2-1_iphoneos-arm.deb
```

**Method 4: Add Procursus Repository** (for newer jailbreaks)

```bash
# Add Procursus repository
echo "deb https://apt.procurs.us/ ./" > /etc/apt/sources.list.d/procursus.list

# Update and install
apt-get update
apt-get install ldid
```

**If all methods fail**, you can still install apps without ldid by using AppSync Unified (see Method 2 below).

### uicache Command Not Found

If `uicache` is not available:

```bash
# Install uikittools
apt-get install uikittools

# Or use alternative refresh method
killall -9 SpringBoard
```

### App Doesn't Appear After Installation

1. **Check if app was copied correctly**:
   ```bash
   ls -la /Applications/
   ```

2. **Verify permissions**:
   ```bash
   chmod -R 755 /Applications/Browser.app
   chown -R mobile:mobile /Applications/Browser.app
   ```

3. **Force refresh**:
   ```bash
   uicache -a
   killall -9 SpringBoard
   # Or reboot
   reboot
   ```

4. **Check Info.plist**:
   ```bash
   cat /Applications/Browser.app/Info.plist | grep CFBundleIdentifier
   ```

---

## Common Issues

### "killed: 9" Error When Launching App

This typically means the app isn't properly signed. Re-sign with ldid:

```bash
cd /Applications/Browser.app
ldid -S Browser
# Or sign all executables
find . -type f -perm +111 -exec ldid -S {} \;
```

### App Crashes on Launch

1. **Check crash logs**:
   ```bash
   ls -lt /var/mobile/Library/Logs/CrashReporter/
   cat /var/mobile/Library/Logs/CrashReporter/Browser*.ips
   ```

2. **Verify all frameworks are signed**:
   ```bash
   cd /Applications/Browser.app
   find . -name "*.dylib" -exec ldid -S {} \;
   find . -name "*.framework" -type d -exec sh -c 'ldid -S "$1/$(basename $1 .framework)"' _ {} \;
   ```

3. **Check dependencies**:
   Some apps may require specific frameworks or libraries. Check the app's documentation.

### Permission Denied Errors

```bash
# Fix ownership
chown -R mobile:mobile /Applications/Browser.app

# Fix permissions
chmod -R 755 /Applications/Browser.app
find /Applications/Browser.app -type f -exec chmod 644 {} \;
find /Applications/Browser.app -type f -perm +111 -exec chmod 755 {} \;
```

### Transfer Failed / SCP Issues

If SCP fails:

```bash
# Option 1: Use alternate port (if SSH is on different port)
scp -P 22 "Browser new.ipa" root@your-apple-tv-ip:/var/root/

# Option 2: Use SFTP
sftp root@your-apple-tv-ip
put "Browser new.ipa" /var/root/
quit

# Option 3: Use curl/wget (if hosted online)
ssh root@your-apple-tv-ip
curl -O http://your-server/Browser_new.ipa

# Option 4: Use Python simple HTTP server
# On your computer (where IPA file is):
python3 -m http.server 8000
# Then on Apple TV:
wget http://your-computer-ip:8000/Browser_new.ipa
```

---

## Quick Reference Commands

### Complete Installation (One-liner approach)

```bash
# On your computer - Transfer file
scp "Browser new.ipa" root@192.168.1.193:/var/root/

# On Apple TV - Install
ssh root@192.168.1.193 'cd /var/root && \
  mkdir -p ipa_temp && cd ipa_temp && \
  unzip "../Browser new.ipa" && \
  cd Payload && \
  find *.app -type f -perm +111 -exec ldid -S {} \; && \
  cp -r *.app /Applications/ && \
  chmod -R 755 /Applications/*.app && \
  chown -R mobile:mobile /Applications/*.app && \
  uicache -a && \
  killall -9 SpringBoard'
```

### Remove/Uninstall an App

```bash
# Remove the app
rm -rf /Applications/Browser.app

# Refresh app list
uicache -a
killall -9 SpringBoard
```

---

## Additional Notes

### About the IPA Files in This Repository

This repository contains several browser IPA files:

- **Browser_trollsigned.ipa** - Pre-signed with TrollStore method
- **Browser copy.ipa** - Unsigned version, needs signing with ldid
- **Browser_unsigned copy.ipa** - Another unsigned variant
- **Safari.ipa** - Safari browser port for Apple TV

The unsigned versions will need to be signed using the ldid method described above.

### About ldid

`ldid` (Link Identity Editor) is a tool that modifies Mach-O binaries to add code signatures. On jailbroken devices, it's used to sign apps so they can run without official Apple signatures.

### Security Considerations

- Only install IPAs from trusted sources
- Be aware that unsigned/modified apps may have security risks
- Keep your jailbreak tools and packages updated
- Change the default SSH password (`alpine`) immediately after jailbreak

---

## Related Documentation

- [CHECKRA1N_NITOTV_GUIDE.md](CHECKRA1N_NITOTV_GUIDE.md) - Complete jailbreak guide
- [NITOTV_SOURCES.txt](NITOTV_SOURCES.txt) - Quick reference for sources
- [README.md](README.md) - Repository overview

---

## Credits

This guide is maintained for the Apple TV jailbreak community. Contributions welcome!
