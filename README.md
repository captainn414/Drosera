ا# Drosera  راهنمای نصب و اجرای نود 

⚙️ا گرفتن rpc  از Alchemy 

وارد سایت https://www.alchemy.com/ شوید 

ابتدا لاگین (ورود) کنید یا اگر حساب ندارید، ثبت‌نام انجام دهید.

مرحله بعد  rpc  رو از اینجا بگیرید https://dashboard.alchemy.com/chains/eth?network=ETH_HOLESKY

💻 حداقل سیستم پیشنهادی برای اجرای نود Drosera:

    پردازنده (CPU): حداقل ۲ هسته

    رم (RAM): حداقل ۴ گیگابایت

    فضای ذخیره‌سازی (Storage): حداقل ۲۰ گیگابایت (ترجیحاً SSD برای عملکرد بهتر)
**#1️نصب پیش‌نیازها (روی Ubuntu 24.04.2 LTS)**
 
  
📦 به‌روزرسانی سیستم:
```
sudo apt update && sudo apt upgrade -y
 ``` 


📥 نصب پکیج‌های مورد نیاز:
 ``` 
sudo apt install -y curl ufw iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli \
libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip
 ``` 


🐳 نصب Docker (در صورتی که از قبل نصب نکردی)

اگر Docker روی سیستم شما نصب نیست، از دستورات زیر استفاده کن:
 ``` 
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove -y $pkg; done

sudo apt install -y ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
$(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update && sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo docker run hello-world

 ``` 
**2️⃣ تنظیم محیط (Environment Setup)**
✅ نصب Drosera CLI:
```
curl -L https://app.drosera.io/install | bash
source ~/.bashrc
droseraup
```
