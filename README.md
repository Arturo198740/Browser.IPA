# Browser.IPA

Apple TV 4 Browser Applications and Jailbreak Resources

## Overview

This repository contains browser IPA files for Apple TV 4 and comprehensive documentation for jailbreaking older Apple TV 4 devices with checkra1n or ChimeraTV, and installing/updating Nito TV.

## Contents

### Browser Applications
- `Browser_trollsigned.ipa` - TrollStore signed browser for Apple TV
- `Browser copy.ipa` - Unsigned browser copy
- `Browser_unsigned copy.ipa` - Unsigned browser variant
- `Safari.ipa` - Safari browser for Apple TV

### Documentation
- **[CHECKRA1N_NITOTV_GUIDE.md](CHECKRA1N_NITOTV_GUIDE.md)** - Complete guide for:
  - Jailbreaking Apple TV 4 with checkra1n or ChimeraTV
  - Installing Nito TV package manager
  - **Updating Nito TV** (in-app and SSH methods)
  - Official Nito TV sources and additional repositories
  - **tvOS 12.1.2 compatibility fixes**
  - Security best practices
  - Troubleshooting common issues

- **[IPA_INSTALLATION_GUIDE.md](IPA_INSTALLATION_GUIDE.md)** - Complete guide for:
  - **Installing IPA files via terminal on jailbroken Apple TV**
  - Using ldid to sign IPA files
  - Transferring files with SCP
  - Installing browser IPAs included in this repository
  - Troubleshooting installation issues

- **[NITOTV_SOURCES.txt](NITOTV_SOURCES.txt)** - Quick reference for:
  - Official repository URLs
  - Update commands
  - tvOS 12.1.2 specific fixes

## Quick Start

### Jailbreak Options

Choose the best jailbreak for your tvOS version:

#### Checkra1n (tvOS 12.0-13.2)
- Best for tvOS 12.0-13.2
- Requires Mac or Linux
- May need troubleshooting on tvOS 12.1.2

#### ChimeraTV (tvOS 12.0-12.4)
- Better for tvOS 12.1.2
- Works on Apple TV 4 and 4K
- Includes Sileo and Nito TV

### For Jailbreaking and Installing Nito TV

1. Read the complete guide: [CHECKRA1N_NITOTV_GUIDE.md](CHECKRA1N_NITOTV_GUIDE.md)
2. **Checkra1n**: https://checkra.in/
3. **ChimeraTV**: https://chimera.coolstar.org/
4. Official Nito TV Repository: `https://nitosoft.com/atv/` or `https://repo.nito.tv/`

### Updating Nito TV

If your Nito TV is outdated:

**Method 1** - Within Nito TV app: Settings → Updates → Refresh Sources

**Method 2** - Via SSH:
```bash
ssh root@your-apple-tv-ip
apt-get update && apt-get upgrade
```

**If you get SSL certificate errors**, use HTTP instead:
```bash
# Edit sources to use HTTP
nano /etc/apt/sources.list.d/nito.list
# Change https:// to http:// for all repos
```

See the [complete guide](CHECKRA1N_NITOTV_GUIDE.md#updating-nito-tv) for detailed instructions.

### Installing IPA Files on Jailbroken Apple TV

To install the browser IPA files from this repository on your jailbroken Apple TV:

**Quick Method** - Via terminal:
```bash
# 1. Transfer IPA to Apple TV
scp "Browser new.ipa" root@your-apple-tv-ip:/var/root/

# 2. SSH in and install with ldid
ssh root@your-apple-tv-ip

# 3. Install ldid if not available
# If "apt-get install ldid" fails, use:
curl -L -O https://github.com/ProcursusTeam/ldid/releases/download/v2.1.5-procursus7/ldid_2.1.5-procursus7_iphoneos-arm.deb
dpkg -i ldid_2.1.5-procursus7_iphoneos-arm.deb

# 4. Extract and sign IPA
unzip "Browser new.ipa" -d /tmp/install/
cd /tmp/install/Payload
ldid -S *.app/*         # Sign the app
cp -r *.app /Applications/
chmod -R 755 /Applications/*.app
uicache -a && killall -9 SpringBoard
```

See the [IPA Installation Guide](IPA_INSTALLATION_GUIDE.md) for complete instructions, troubleshooting, and alternative methods.

### Official Sources Only

⚠️ **IMPORTANT**: Only use official Nito TV repositories:
```
https://nitosoft.com/atv/
https://repo.nito.tv/
```

Avoid unofficial sources, mirrors, or modified repositories to ensure security and stability.

### Additional Repositories

For more packages, see the [sources section](CHECKRA1N_NITOTV_GUIDE.md#additional-verified-repositories) in the complete guide.

## Compatibility

### Checkra1n
- **Device**: Apple TV 4 (HD) - 4th Generation
- **tvOS**: 12.0 - 13.2
- **Note**: tvOS 12.1.2 may require troubleshooting (see guide)

### ChimeraTV
- **Device**: Apple TV 4 (HD) and Apple TV 4K
- **tvOS**: 12.0 - 12.2 and 12.4
- **Better compatibility** with tvOS 12.1.2

## Resources

- [Complete Checkra1n & Nito TV Guide](CHECKRA1N_NITOTV_GUIDE.md)
- [IPA Installation Guide](IPA_INSTALLATION_GUIDE.md) - **NEW: Install browser IPAs via terminal**
- [Quick Reference: Sources & Updates](NITOTV_SOURCES.txt)
- [Official Checkra1n Website](https://checkra.in/)
- [Official ChimeraTV Website](https://chimera.coolstar.org/)
- [iOS Guide for Apple TV](https://ios.cfw.guide/installing-checkra1n-tv/)
- [ChimeraTV Guide](https://ios.cfw.guide/installing-chimeratv/)
- [Nito TV Official Repository](https://nitosoft.com/atv/)

## Disclaimer

This repository is for educational purposes. Jailbreaking may void warranties and violate terms of service. Users are responsible for understanding local laws and accepting modification risks.

## Contributing

Contributions welcome! Please ensure all sources and information reference only official, verified repositories and tools.
