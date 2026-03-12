# Checkra1n Apple TV 4 Jailbreak & Nito TV Sources Guide

## Overview
This guide provides comprehensive instructions for jailbreaking Apple TV 4 (HD) using checkra1n and installing Nito TV with official sources. This is specifically designed for older Apple TV 4 devices running compatible tvOS versions.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Official Nito TV Repository Source](#official-nito-tv-repository-source)
- [Step-by-Step Jailbreak Instructions](#step-by-step-jailbreak-instructions)
- [Installing Nito TV](#installing-nito-tv)
- [Adding Sources to Nito TV](#adding-sources-to-nito-tv)
- [Security Best Practices](#security-best-practices)
- [Troubleshooting](#troubleshooting)
- [Additional Resources](#additional-resources)

---

## Prerequisites

Before you begin, ensure you have:

- **Apple TV 4 (HD)** - 4th Generation model
- **Compatible tvOS version** - tvOS 12.0 to 13.2 (check compatibility at https://checkra.in/)
- **Mac or Linux computer** - Required to run checkra1n
- **USB-C cable** - To connect Apple TV to your computer
- **Same network** - Both devices should be on the same local network
- **SSH client** - Terminal (Mac/Linux) or SSH client software

---

## Official Nito TV Repository Source

### ⚠️ IMPORTANT: Use Only Official Sources

The **only legitimate and verified** Nito TV repository source is:

```
https://nitosoft.com/atv/
```

### Why Official Sources Matter
- **Security**: Unofficial sources may contain malware or compromised packages
- **Stability**: Official repos ensure compatibility and tested packages
- **Support**: Community support is only available for official sources
- **Updates**: Official sources receive regular updates and security patches

### ❌ Avoid These:
- Third-party mirrors
- Modified repositories
- Unofficial "modded" repos
- Random forum links
- Piracy sources

---

## Step-by-Step Jailbreak Instructions

### Step 1: Download Checkra1n

1. Visit the official checkra1n website: https://checkra.in/
2. Download the latest version for your operating system (macOS or Linux)
3. For detailed platform-specific instructions, see: https://ios.cfw.guide/installing-checkra1n-tv/macos/

### Step 2: Prepare Your Apple TV 4

1. Connect your Apple TV 4 to your computer using a USB-C cable
2. Launch the checkra1n application on your computer
3. Follow the on-screen instructions to put your Apple TV into DFU (Device Firmware Update) mode

### Step 3: Enter DFU Mode

The checkra1n tool will guide you through entering DFU mode:
1. Disconnect the power cable from your Apple TV
2. Connect the USB-C cable to your Apple TV
3. Hold the Menu and Volume Down buttons
4. Follow the prompts in checkra1n

### Step 4: Run the Jailbreak

1. Click "Start" in the checkra1n application
2. Wait for the jailbreak process to complete (usually 2-5 minutes)
3. Your Apple TV will reboot automatically
4. The checkra1n loader app should appear on your home screen

---

## Installing Nito TV

After successfully jailbreaking your Apple TV 4, follow these steps to install Nito TV:

### Method 1: Using SSH (Recommended)

1. **Get Your Apple TV's IP Address**
   - On Apple TV: Go to Settings → Network
   - Note the IP address displayed

2. **Connect via SSH**
   ```bash
   ssh root@your-apple-tv-ip
   ```
   Or use the hostname:
   ```bash
   ssh root@Apple-TV.local
   ```

   Default password: `alpine`

3. **Change the Default Password (CRITICAL)**
   ```bash
   passwd
   ```
   Enter a new secure password when prompted.

4. **Download and Install Nito TV**
   ```bash
   wget http://nitosoft.com/ATV4/installNTV.sh
   chmod +x installNTV.sh
   ./installNTV.sh
   ```

5. **Wait for Installation**
   - The script will download and install Nito TV
   - Your Apple TV may reboot during or after installation
   - This process typically takes 2-5 minutes

6. **Verify Installation**
   - After reboot, check your Apple TV home screen
   - Nito TV should appear as an app icon

### Method 2: Using Checkra1n Loader

Some versions of checkra1n include built-in Nito TV installation:
1. Open the checkra1n loader app on your Apple TV
2. Look for a Nito TV installation option
3. Follow the on-screen prompts

---

## Adding Sources to Nito TV

### Accessing Nito TV

1. Launch Nito TV from your Apple TV home screen
2. Navigate through the interface using your Apple TV remote

### Built-in Source

Nito TV comes pre-configured with the official repository:
```
https://nitosoft.com/atv/
```

### Managing Sources in Nito TV

Nito TV functions similarly to Cydia on iOS:
- **Browse Packages**: View available tweaks, apps, and utilities
- **Install Packages**: Download and install apps directly through Nito TV
- **Manage Sources**: Add or remove repositories (advanced users)
- **Update Packages**: Keep installed packages up to date

### Popular Packages Available

Through the official Nito TV repository, you can install:
- Web browsers (like the ones in this repository)
- Media players
- Emulators
- File managers
- System utilities
- SSH tools
- Development utilities

---

## Security Best Practices

### 1. Change Default Password
**CRITICAL**: The default SSH password is `alpine`. Change it immediately:
```bash
ssh root@your-apple-tv-ip
passwd
```

### 2. Use Only Official Sources
- Stick to https://nitosoft.com/atv/
- Verify URLs before adding sources
- Check community forums for verification

### 3. Keep Software Updated
- Update checkra1n when new versions are released
- Keep Nito TV updated through the app
- Update installed packages regularly

### 4. Backup Before Modifications
- Document your installed packages
- Note any custom configurations
- Be prepared to restore if needed

### 5. Network Security
- Use strong WiFi passwords
- Consider network segmentation for jailbroken devices
- Disable SSH when not in use (optional)

### 6. Verify Package Sources
- Only install packages from trusted developers
- Read package descriptions carefully
- Check community reviews and feedback

---

## Troubleshooting

### Jailbreak Won't Complete
- Ensure you're using the latest checkra1n version
- Verify your tvOS version is compatible (12.0-13.2)
- Try a different USB-C cable
- Restart both devices and try again

### Can't SSH Into Apple TV
- Verify both devices are on the same network
- Check the IP address is correct
- Ensure the jailbreak completed successfully
- Try using the hostname: `ssh root@Apple-TV.local`

### Nito TV Won't Install
- Check your internet connection
- Verify the installation script downloaded completely
- Try downloading the script again
- Check available storage on your Apple TV

### Nito TV App Crashes
- Reboot your Apple TV
- Re-run the Nito TV installation script
- Check for updates to Nito TV
- Verify you're using the official repository

### Apple TV Won't Boot After Jailbreak
- Try rebooting by holding Menu + Home buttons
- Re-run checkra1n to re-jailbreak
- If persistent, restore tvOS through iTunes/Finder (removes jailbreak)

### Packages Won't Install
- Ensure you have sufficient storage space
- Check that sources are properly configured
- Verify internet connectivity
- Try refreshing sources in Nito TV

---

## Additional Resources

### Official Links
- **Checkra1n Official**: https://checkra.in/
- **Nito TV Official**: https://nitosoft.com/atv/
- **iOS Guide for Apple TV**: https://ios.cfw.guide/installing-checkra1n-tv/
- **macOS-specific Guide**: https://ios.cfw.guide/installing-checkra1n-tv/macos/

### Community Resources
- **r/Jailbreak Subreddit**: For community support and discussions
- **Checkra1n Discord**: Official community Discord server
- **iOS Guide**: Comprehensive jailbreak documentation

### Video Tutorials
- Search for "Jailbreak Apple TV 4 checkra1n" on YouTube for visual guides
- Look for recent tutorials (2023 or newer)

### Important Notes
- Jailbreaking voids your warranty
- Some streaming services may not work on jailbroken devices
- Apple updates may break the jailbreak
- Always backup important data before proceeding

---

## Compatibility Information

### Supported Apple TV Models
- Apple TV 4 (HD) - 4th Generation
- Model: A1625 (2015)

### Supported tvOS Versions
- tvOS 12.0 - 13.2 (with checkra1n 0.12.0+)
- Check https://checkra.in/ for latest compatibility

### Not Currently Supported
- Apple TV 4K (5th Generation) - Not compatible with checkra1n
- Apple TV 4K (6th Generation) - Not compatible with checkra1n
- tvOS 14+ - Limited or no support

---

## Legal Disclaimer

This guide is provided for educational purposes only. Jailbreaking may:
- Void your device warranty
- Violate terms of service
- Cause stability or security issues
- Be prohibited in some jurisdictions

Users are responsible for:
- Understanding local laws and regulations
- Accepting risks of device modification
- Following terms of service for apps and services
- Using jailbreak tools responsibly

---

## Contributing

Found an issue or have improvements? This guide is maintained for the Apple TV jailbreak community. Please ensure all suggestions use only official, verified sources.

---

## Changelog

### 2026-03-12
- Initial comprehensive guide created
- Added official Nito TV source information
- Included security best practices
- Added troubleshooting section

---

**Remember**: Always use official sources and practice good security hygiene. The only verified Nito TV repository is `https://nitosoft.com/atv/`.
