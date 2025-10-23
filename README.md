# 🖥️ Free Remote Desktop Access via GitHub Actions

[![GitHub Actions](https://img.shields.io/badge/GitHub-Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)](https://github.com/features/actions)
[![Cloudflare](https://img.shields.io/badge/Cloudflare-Tunnel-F38020?style=for-the-badge&logo=cloudflare&logoColor=white)](https://www.cloudflare.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](LICENSE)

> **Access full Windows, macOS, and Linux desktop environments for FREE using GitHub Actions and Cloudflare Tunnels - No domain required, No authentication needed!**

---

## 📋 Table of Contents

- [Features](#-features)
- [Supported Operating Systems](#-supported-operating-systems)
- [Prerequisites](#-prerequisites)
- [Quick Start](#-quick-start)
- [Setup Instructions](#-setup-instructions)
- [Client Connection Guide](#-client-connection-guide)
  - [Windows Clients](#-windows-clients)
  - [macOS Clients](#-macos-clients)
  - [Linux Clients](#-linux-clients)
  - [Mobile Devices](#-mobile-devices)
  - [Termux (Android Linux Environment)](#-termux-android-linux-environment)
- [Network-Wide Access](#-network-wide-access)
- [Specifications](#-specifications)
- [Troubleshooting](#-troubleshooting)
- [Security Notes](#-security-notes)
- [FAQ](#-faq)
- [Contributing](#-contributing)
- [License](#-license)

---

## ✨ Features

- 🆓 **100% Free** - No credit card, no paid subscriptions
- 🚀 **Instant Setup** - One-click deployment via GitHub Actions
- 🔒 **Secure Tunneling** - Cloudflare encrypted connections
- 🌐 **No Domain Required** - Automatic TryCloudflare subdomain
- 💻 **Full Desktop Access** - Complete GUI environments
- 📱 **Multi-Platform Support** - Connect from any device
- ⏱️ **6 Hours Runtime** - Per workflow session
- 🔄 **Unlimited Restarts** - Run as many sessions as needed

---

## 🖥️ Supported Operating Systems

| OS | Protocol | Port | Desktop Environment |
|---|---|---|---|
| **Windows Server 2022** | RDP | 3389 | Full GUI |
| **macOS 12+ (Monterey/Ventura)** | VNC | 5900 | Native macOS |
| **Ubuntu 22.04 LTS** | VNC | 5901 | XFCE4 |

---

## 📦 Prerequisites

### Server Side (Automatic)
- GitHub account
- Repository with GitHub Actions enabled

### Client Side (Manual Setup Required)
- **Cloudflared client** installed on your local machine
- **RDP/VNC client** based on target OS

---

## 🚀 Quick Start

### Step 1: Setup Repository

1. **Fork/Create** this repository
2. Go to **Actions** tab
3. Select your desired workflow:
   - `WINDOWS RDP - CLOUDFLARE`
   - `macOS VNC - CLOUDFLARE`
   - `LINUX DESKTOP - CLOUDFLARE`
4. Click **Run workflow**
5. Wait 2-3 minutes for initialization

### Step 2: Get Tunnel URL

Check workflow logs and copy the **Cloudflare Tunnel URL**:
```
https://example-random-subdomain.trycloudflare.com
```

### Step 3: Connect

Follow the [Client Connection Guide](#-client-connection-guide) below based on your device.

---

## 🛠️ Setup Instructions

### Option 1: Using Pre-Made Workflows

Copy the appropriate workflow file to `.github/workflows/` in your repository:

- **Windows:** `windows-rdp.yml`
- **macOS:** `macos-vnc.yml`
- **Linux:** `linux-desktop.yml`

### Option 2: Manual Creation

Create a new file in `.github/workflows/` and paste the workflow code for your desired OS.

**Default Credentials:**
- **Username:** `runneradmin` (Windows) / `vncuser` (macOS) / N/A (Linux)
- **Password:** `P@ssw0rd123!` (All systems)

> ⚠️ **Change the password** in workflow files before running!

---

## 🔌 Client Connection Guide

### Prerequisites for All Clients

Install **cloudflared** on your local machine:

**Windows:**
```
# Download from GitHub Releases
https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-windows-amd64.exe
```

**macOS:**
```
brew install cloudflare/cloudflare/cloudflared
```

**Linux:**
```
wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64
chmod +x cloudflared-linux-amd64
sudo mv cloudflared-linux-amd64 /usr/local/bin/cloudflared
```

---

## 💻 Windows Clients

### Connecting to Windows RDP

#### Step 1: Start Local Tunnel
```
cloudflared access tcp --hostname <your-tunnel-url> --url localhost:3389
```

**Example:**
```
cloudflared access tcp --hostname admitted-detected-lexington.trycloudflare.com --url localhost:3389
```

#### Step 2: Open Remote Desktop
- Press **Windows + R**
- Type: `mstsc`
- Press **Enter**

#### Step 3: Enter Connection Details
- **Computer:** `localhost:3389`
- **Username:** `runneradmin`
- **Password:** `P@ssw0rd123!`

#### Step 4: Connect
Click **Connect** and accept any certificate warnings.

---

### Connecting to macOS VNC from Windows

#### Step 1: Start Local Tunnel
```
cloudflared access tcp --hostname <your-macos-tunnel-url> --url localhost:5900
```

#### Step 2: Download VNC Viewer
Install **RealVNC Viewer** or **TightVNC Viewer**:
- RealVNC: https://www.realvnc.com/en/connect/download/viewer/

#### Step 3: Connect
- Open VNC Viewer
- **Server:** `localhost:5900`
- **Password:** `P@ssw0rd123!`

---

### Connecting to Linux Desktop from Windows

Same as macOS VNC, but use port **5901**:
```
cloudflared access tcp --hostname <your-linux-tunnel-url> --url localhost:5901
```

Then connect with VNC Viewer to `localhost:5901`.

---

## 🍎 macOS Clients

### Connecting to Windows RDP from Mac

#### Step 1: Start Local Tunnel
```
cloudflared access tcp --hostname <your-windows-tunnel-url> --url localhost:3389
```

#### Step 2: Install Microsoft Remote Desktop
Download from Mac App Store:
- **Microsoft Remote Desktop** (Free)

#### Step 3: Add Connection
- Open Microsoft Remote Desktop
- Click **+ Add PC**
- **PC name:** `localhost:3389`
- **User account:** Add credentials
  - Username: `runneradmin`
  - Password: `P@ssw0rd123!`

#### Step 4: Connect
Double-click the connection to start.

---

### Connecting to macOS VNC from Mac

#### Step 1: Start Local Tunnel
```
cloudflared access tcp --hostname <your-macos-tunnel-url> --url localhost:5900
```

#### Step 2: Use Built-in Screen Sharing
```
open vnc://localhost:5900
```

Or:
- Open **Finder**
- Press **Command + K**
- Enter: `vnc://localhost:5900`
- Password: `P@ssw0rd123!`

---

### Connecting to Linux Desktop from Mac

Same as macOS VNC, but use port **5901**:
```
cloudflared access tcp --hostname <your-linux-tunnel-url> --url localhost:5901
open vnc://localhost:5901
```

---

## 🐧 Linux Clients

### Connecting to Any OS from Linux

#### Step 1: Start Local Tunnel
```
# For Windows RDP
cloudflared access tcp --hostname <tunnel-url> --url localhost:3389

# For macOS/Linux VNC
cloudflared access tcp --hostname <tunnel-url> --url localhost:5900
```

#### Step 2: Install RDP/VNC Client

**For Windows RDP:**
```
sudo apt install remmina  # Ubuntu/Debian
sudo dnf install remmina  # Fedora
```

**For macOS/Linux VNC:**
```
sudo apt install tigervnc-viewer  # Ubuntu/Debian
sudo dnf install tigervnc         # Fedora
```

#### Step 3: Connect

**RDP (Windows):**
```
remmina -c rdp://localhost:3389
# Or use GUI: Protocol=RDP, Server=localhost:3389
```

**VNC (macOS/Linux):**
```
vncviewer localhost:5900  # or 5901 for Linux
```

---

## 📱 Mobile Devices

### Android

#### For Windows RDP

1. **Install Microsoft Remote Desktop**
   - **Google Play Store:** [Microsoft Remote Desktop](https://play.google.com/store/apps/details?id=com.microsoft.rdc.androidx)
   - **Alternative APK:** [APKMirror - Microsoft Remote Desktop](https://www.apkmirror.com/apk/microsoft-corporation/microsoft-remote-desktop/)

2. **Setup Cloudflared on PC**
   - Run cloudflared on a PC in your network
   ```
   cloudflared access tcp --hostname <tunnel-url> --url 0.0.0.0:3389
   ```

3. **Find PC IP Address**
   ```
   ipconfig  # Windows
   ifconfig  # Linux/Mac
   ```

4. **Connect from Android**
   - Open Microsoft Remote Desktop app
   - Tap **+** → **Desktop**
   - **PC name:** `192.168.x.x:3389` (your PC IP)
   - **User account:** runneradmin / P@ssw0rd123!
   - Tap **Save** and connect

#### For macOS/Linux VNC

1. **Install VNC Viewer**
   - **Google Play Store:** [VNC Viewer](https://play.google.com/store/apps/details?id=com.realvnc.viewer.android)
   - **Alternative APK:** [APKMirror - VNC Viewer](https://www.apkmirror.com/apk/realvnc-limited/vnc-viewer-remote-desktop/)

2. **Setup Cloudflared on PC (same network)**
   ```
   cloudflared access tcp --hostname <tunnel-url> --url 0.0.0.0:5900
   ```

3. **Connect from Android**
   - Open VNC Viewer app
   - Tap **+**
   - **Address:** `192.168.x.x:5900` (your PC IP)
   - **Name:** Any name
   - **Password:** P@ssw0rd123!

---

### iOS (iPhone/iPad)

#### For Windows RDP

1. **Install Microsoft Remote Desktop**
   - **Apple App Store:** [Microsoft Remote Desktop](https://apps.apple.com/app/microsoft-remote-desktop/id714464092)

2. **Setup Cloudflared on Mac/PC**
   ```
   cloudflared access tcp --hostname <tunnel-url> --url 0.0.0.0:3389
   ```

3. **Connect from iOS**
   - Open app → Tap **+** → **Add PC**
   - **PC name:** Your Mac/PC IP (192.168.x.x:3389)
   - **User account:** runneradmin / P@ssw0rd123!

#### For macOS/Linux VNC

1. **Install VNC Viewer**
   - **Apple App Store:** [VNC Viewer](https://apps.apple.com/app/vnc-viewer-remote-desktop/id352019548)

2. **Setup and Connect**
   - Same process as Android VNC
   - Use port 5900 for macOS, 5901 for Linux

---

## 📱 Termux (Android Linux Environment)

### Install Termux Officially

**🚨 IMPORTANT: Don't use Google Play Store version (outdated & broken)**

#### Option 1: F-Droid (Recommended)
1. **Download F-Droid:** [F-Droid Official](https://f-droid.org/)
2. **Install F-Droid APK** on your Android device
3. **Search for "Termux"** in F-Droid app
4. **Install Termux:** [Termux on F-Droid](https://f-droid.org/en/packages/com.termux/)

#### Option 2: GitHub Releases
1. **Visit GitHub:** [Termux Releases](https://github.com/termux/termux-app/releases)
2. **Download latest APK:** `termux-app_vX.X.X+github-debug_universal.apk`
3. **Enable "Install from Unknown Sources"** in Android settings
4. **Install the APK**

---

### Using Termux for Remote Desktop Access

#### Step 1: Setup Termux Environment
```bash
# Update packages
pkg update && pkg upgrade

# Install required packages
pkg install wget curl git
```

#### Step 2: Install Cloudflared in Termux
```bash
# Download cloudflared for ARM64 (most modern Android devices)
wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-arm64

# Make it executable
chmod +x cloudflared-linux-arm64

# Move to PATH
mv cloudflared-linux-arm64 $PREFIX/bin/cloudflared

# Verify installation
cloudflared --version
```

#### Step 3: Connect to Remote Desktop

**For Windows RDP:**
```bash
# Start tunnel
cloudflared access tcp --hostname <your-tunnel-url> --url localhost:3389

# Keep this terminal open, open new session
# Install RDP client
pkg install freerdp

# Connect to Windows
xfreerdp /v:localhost:3389 /u:runneradmin /p:P@ssw0rd123!
```

**For macOS/Linux VNC:**
```bash
# Start tunnel
cloudflared access tcp --hostname <your-tunnel-url> --url localhost:5900

# Install VNC client
pkg install tigervnc

# Connect to VNC
vncviewer localhost:5900
# Enter password when prompted: P@ssw0rd123!
```

#### Step 4: GUI Access in Termux (Optional)

For better experience with graphical applications:

```bash
# Install VNC server for Termux
pkg install x11-repo
pkg install tigervnc xfce4

# Start VNC server
vncserver :1

# In another session, connect to your remote desktop
cloudflared access tcp --hostname <tunnel-url> --url localhost:5900
```

---

### Termux Troubleshooting

**Issue: "Permission denied" when installing cloudflared**
```bash
# Fix permissions
termux-setup-storage
chmod +x cloudflared-linux-arm64
```

**Issue: "Command not found" for cloudflared**
```bash
# Check if binary is in correct location
ls -la $PREFIX/bin/cloudflared

# If not there, move it manually
cp cloudflared-linux-arm64 $PREFIX/bin/cloudflared
```

**Issue: VNC connection fails**
```bash
# Check if tunnel is running
ps aux | grep cloudflared

# Restart tunnel if needed
pkill cloudflared
cloudflared access tcp --hostname <tunnel-url> --url localhost:5900 &
```

---

## 🌐 Network-Wide Access

To allow connections from **any device on your local network** (not just localhost):

### Modify Cloudflared Command

Instead of `localhost`, use `0.0.0.0`:

```
# Windows RDP
cloudflared access tcp --hostname <tunnel-url> --url 0.0.0.0:3389

# macOS VNC
cloudflared access tcp --hostname <tunnel-url> --url 0.0.0.0:5900

# Linux VNC
cloudflared access tcp --hostname <tunnel-url> --url 0.0.0.0:5901
```

### Find Your PC's Local IP

**Windows:**
```
ipconfig
```

**macOS/Linux:**
```
ifconfig
# or
ip addr show
```

Look for **IPv4 Address** (e.g., `192.168.1.100`)

### Connect from Other Devices

Use your PC's IP instead of localhost:
- **RDP:** `192.168.1.100:3389`
- **VNC:** `192.168.1.100:5900`

### Allow Firewall Access

**Windows:**
```
New-NetFirewallRule -DisplayName "Cloudflared RDP" -Direction Inbound -LocalPort 3389 -Protocol TCP -Action Allow
```

**Linux:**
```
sudo ufw allow 5901/tcp
```

---

## 📊 Specifications

### Windows Server 2022
- **CPU:** 4 cores (Intel Xeon)
- **RAM:** 16GB
- **Storage:** 14GB SSD
- **OS:** Windows Server 2022 Datacenter
- **Pre-installed:** Visual Studio Build Tools, Git, PowerShell

### macOS Monterey/Ventura
- **CPU:** 3 cores
- **RAM:** 14GB
- **Storage:** 14GB SSD
- **OS:** macOS 12+ (Monterey/Ventura)
- **Pre-installed:** Xcode, Homebrew, Git

### Ubuntu 22.04 LTS
- **CPU:** 4 cores
- **RAM:** 16GB
- **Storage:** 14GB SSD
- **OS:** Ubuntu 22.04 LTS
- **Desktop:** XFCE4
- **Pre-installed:** Docker, Git, build-essential

### Session Limits
- **Runtime:** 6 hours per workflow
- **Concurrent Jobs:** 20 (Free tier)
- **Monthly Minutes:** 2,000 minutes (Free tier)

---

## 🔧 Troubleshooting

### Issue: "Tunnel URL not appearing in logs"

**Solution:**
- Wait 2-3 minutes for full initialization
- Check if cloudflared installed correctly
- Look for separate PowerShell window (Windows)

### Issue: "Connection refused" or "Cannot connect"

**Solution:**
1. Verify cloudflared is running on client machine
2. Check if correct port is used (3389/5900/5901)
3. Ensure tunnel URL is correct
4. Check firewall settings

### Issue: "Invalid password" or "Authentication failed"

**Solution:**
- Default password: `P@ssw0rd123!`
- Check if password was changed in workflow
- For macOS VNC, try lowercase password

### Issue: "Websocket listener not starting"

**Solution:**
```
# Kill existing cloudflared processes
taskkill /F /IM cloudflared.exe  # Windows
killall cloudflared              # Mac/Linux
pkill cloudflared                # Termux

# Restart cloudflared
cloudflared access tcp --hostname <url> --url localhost:3389
```

### Issue: Mobile app cannot connect

**Solution:**
- Ensure cloudflared uses `0.0.0.0` binding
- Verify mobile device is on same WiFi network
- Use PC's local IP, not localhost
- Check PC firewall allows incoming connections

### Issue: Termux cloudflared not working

**Solution:**
- Check ARM architecture: `uname -m` (should be aarch64 or armv7l)
- Download correct binary for your architecture
- Ensure proper permissions: `chmod +x cloudflared`

---

## 🔒 Security Notes

### Best Practices

1. **Change default password** in workflow files
2. **Don't share tunnel URLs** publicly
3. **Use strong passwords** (12+ characters, mixed case, numbers, symbols)
4. **Monitor workflow logs** for suspicious activity
5. **Delete workflows** when not in use

### Security Features

- ✅ **Encrypted tunnels** via Cloudflare
- ✅ **Temporary URLs** - expire after session ends
- ✅ **No public exposure** - requires cloudflared client
- ✅ **GitHub authentication** required to run workflows

### Important Notes

- Tunnel URLs are **public** but require cloudflared client
- Sessions are **temporary** (max 6 hours)
- **Don't store sensitive data** on these machines
- **GitHub may rate-limit** excessive usage

---

## ❓ FAQ

**Q: Is this really free?**
A: Yes! GitHub Actions provides 2,000 free minutes/month. Cloudflare Tunnels are free forever.

**Q: Can I use this for production workloads?**
A: No, this is for testing/development only. Sessions are temporary and limited.

**Q: How long can I use the desktop?**
A: Maximum 6 hours per session. You can restart unlimited times.

**Q: Can multiple people connect to the same session?**
A: Yes, but performance may degrade with multiple connections.

**Q: What happens to my data when session ends?**
A: Everything is deleted. GitHub Actions runners are ephemeral.

**Q: Can I install custom software?**
A: Yes! You have admin/sudo access. Add installation steps to workflow.

**Q: Does this work in my country?**
A: Yes, if you can access GitHub and Cloudflare.

**Q: Can I access this from anywhere?**
A: Yes, as long as you have the tunnel URL and cloudflared client installed.

**Q: Can I use this on rooted/jailbroken devices?**
A: Yes, but be careful with security. Don't store sensitive data.

**Q: Why not use Google Play Store Termux?**
A: Play Store version is outdated (Android 7 target) and has many broken features. F-Droid version is actively maintained.

---

## 🤝 Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

### Areas for Improvement

- Additional OS support
- Automated testing
- Performance optimizations
- Documentation improvements
- Security enhancements
- Mobile app integration guides
- Termux automation scripts

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- [GitHub Actions](https://github.com/features/actions) - Free CI/CD platform
- [Cloudflare Tunnels](https://www.cloudflare.com/products/tunnel/) - Secure tunneling service
- [AnimMouse/setup-cloudflared](https://github.com/AnimMouse/setup-cloudflared) - GitHub Action for cloudflared
- [Termux Team](https://termux.dev/) - Android Linux environment
- [F-Droid](https://f-droid.org/) - Open source Android app repository

---

## 📞 Support

Found this helpful? Give it a ⭐!

For issues or questions:
- Open an [Issue](../../issues)
- Check [Discussions](../../discussions)
- Read the [Troubleshooting](#-troubleshooting) section

---

<div align="center">

### Built with ❤️ by Sandeep Gaddam

**If this project helped you, consider giving it a ⭐ star!**

[![GitHub followers](https://img.shields.io/github/followers/UnQOfficial?style=social)](https://github.com/UnQOfficial)

---

**Made with 💻 and lots of ☕**

</div>