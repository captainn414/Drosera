# راهنمای نصب و اجرای نود  Drosera  
⚙️ا گرفتن rpc  از Alchemy 

وارد سایت https://www.alchemy.com/ شوید 

ابتدا لاگین (ورود) کنید یا اگر حساب ندارید، ثبت‌نام انجام دهید.

مرحله بعد  rpc  رو از اینجا بگیرید https://dashboard.alchemy.com/chains/eth?network=ETH_HOLESKY

💻 حداقل سیستم پیشنهادی برای اجرای نود Drosera:

    پردازنده (CPU): حداقل ۲ هسته

    رم (RAM): حداقل ۴ گیگابایت

    فضای ذخیره‌سازی (Storage): حداقل ۲۰ گیگابایت (ترجیحاً SSD برای عملکرد بهتر)
**1️# نصب پیش‌نیازها (روی Ubuntu 24.04.2 LTS)**
 
  
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
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Test Docker
sudo docker run hello-world

 ``` 
**2️⃣ تنظیم محیط (Environment Setup)**

✅ نصب Drosera CLI:
```
curl -L https://app.drosera.io/install | bash
source ~/.bashrc
droseraup
```
🛠️ نصب Foundry 
```
curl -L https://foundry.paradigm.xyz | bash
source ~/.bashrc
foundryup
```


⚡ نصب Bun
```
curl -fsSL https://bun.sh/install | bash
source ~/.bashrc
```

استقرار قرارداد (Contract) و راه‌اندازی Trap در DROSERA
```
mkdir my-drosera-trap && cd my-drosera-trap
```
⚙️ تنظیم ایمیل در Git
```
git config --global user.email "your_email@example.com"
```


👤 تنظیم نام کاربری در Git

```
git config --global user.name "your_username"
```
  و nitialize Project
  ```
forge init -t drosera-network/trap-foundry-template
```
و Install & build:

```
bun install
forge build
```
این خطا مورد نداره رد کنید برید جلو 
![image](https://github.com/user-attachments/assets/82920843-add0-4e62-999d-5031efa4f118)


🚀 استقرار Trap در Drosera 
```

DROSERA_PRIVATE_KEY=your_private_key drosera apply
  
```

از یک کیف پول استفاده کن که روی شبکه Holesky مقداری ETH داشته باشد.
وقتی ازت سؤال شد، بنویس: ofc


**4️⃣ بررسی Trap در داشبورد**

وارد شو به: app.drosera.io

کیف پول EVM خودت رو متصل کن → در بخش "Traps Owned" بررسی کن.



