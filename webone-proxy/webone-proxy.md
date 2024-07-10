# WebOne Proxy

```
wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
sudo apt update
wget http://ftp.us.debian.org/debian/pool/main/i/icu/libicu63_63.1-6+deb10u3_arm64.deb
dpkg -i libicu63_63.1-6+deb10u3_arm64.deb
wget https://github.com/atauenis/webone/releases/download/v0.15.3/webone.0.15.3.linux-arm64.deb
sudo apt install ./webone.0.15.3.linux-arm64.deb
```