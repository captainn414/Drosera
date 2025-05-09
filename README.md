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
⚙️ تنظیم ایمیل در Git(ایمیل گیت هاب)
```
git config --global user.email "your_email@example.com"
```


👤 تنظیم نام کاربری در Git( یوزرنیم گیت هاب)
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
بعد اینکه  ofc زدید  ادرس trap بهتون میده مثل عکس زیر 

![image](https://github.com/user-attachments/assets/fe75a63e-f53c-4ec1-9105-7ffc6f3c4f25)




**4️⃣ بررسی Trap در داشبورد**

وارد شو به: app.drosera.io

کیف پول EVM خودت رو متصل کن → در بخش "Traps Owned" بررسی کن.
![image](https://github.com/user-attachments/assets/1484ad69-7086-4899-b535-3430e9a1f307)


۵️⃣ #**ارسال Bloom Boost به Trap**

برو به Trap خودت ← روی گزینه "Send Bloom Boost" کلیک کن ومقداری تریوم Holesky ارسال کن.

![image](https://github.com/user-attachments/assets/fdc1ddc9-6278-43a0-856a-031a7ad7f977)

**6-دریافت Sample Block**

```
drosera dryrun
```

خروجی بدین شکل خواهد بود 
![image](https://github.com/user-attachments/assets/1987c104-a057-4137-9d78-37ce4e387241)


# راه‌اندازی اپراتور

**1-وایت‌لیست کردن اپراتور**
```
cd my-drosera-trap
nano drosera.toml
```

بعد  زدن  دستور  این اطلاعات رو میبینید .
```
ethereum_rpc = "https://eth-holesky.g.alchemy.com/v2/your-api-key"
drosera_rpc = "https://relay.testnet.drosera.io"
eth_chain_id = 17000
drosera_address = "0xea08f7d533C2b9A62F40D5326214f39a8E3A32F8"

[traps.mytrap]
path = "out/HelloWorldTrap.sol/HelloWorldTrap.json"
response_contract = "0xdA890040Af0533D98B9F5f8FE3537720ABf83B0C"
response_function = "helloworld(string)"
cooldown_period_blocks = 33
min_number_of_operators = 1
max_number_of_operators = 2
block_sample_size = 10
private_trap = true
address = "generated after dryrun"
whitelist = ["your_wallet_address"]
```
آدرس your_wallet_address را با آدرس عمومی کیف پول EVM خودت جایگزین کن، داخل علامت " "

و به جای ethereum_rpc   اون  rpc که گذفتیم جاگذاری کنید

**2-به‌روزرسانی تنظیمات Trap**
```
DROSERA_PRIVATE_KEY=your_private_key drosera apply
```

اگر خطا خوردید  تو این قسمت بروزرسانی از این استفاده کنید (  اگه نخوردید اینجارو رد کنید )
```
DROSERA_PRIVATE_KEY=your_private_key drosera apply --eth-rpc-url RPC
```

به جای rpc  از rpc که گرفتیم استفاده کنید 


# نصب Drosera Operator CLI
```
cd ~
sudo apt update && sudo apt install -y tar

curl -LO https://github.com/drosera-network/releases/releases/download/v1.17.2/drosera-operator-v1.17.2-x86_64-unknown-linux-gnu.tar.gz
tar -xvf drosera-operator-v1.17.2-x86_64-unknown-linux-gnu.tar.gz

sudo cp drosera-operator /usr/bin
drosera-operator --version
```

 # مرحله بعد نصب   Pull Docker Image
 ```
docker pull ghcr.io/drosera-network/drosera-operator:latest
```

# مرحله بعد Register Operator

```
drosera-operator register --eth-rpc-url https://eth-holesky.g.alchemy.com/v2/your-api-key --eth-private-key your_private_key

```
قسمت های your_private_key و your-api-key  این ها رو اطلاعات خودتون رو میدید

#  باز کردن پورت‌ها (Open Ports)

```
# Enable firewall
sudo ufw allow ssh
sudo ufw allow 22
sudo ufw enable

# Allow Drosera ports
sudo ufw allow 31313/tcp
sudo ufw allow 31314/tcp
```


# ران کردن نود 
```
git clone https://github.com/HeavenOG/Drosera-Network && cd Drosera-Network
cp .env.example .env
nano .env

```
قسمتی که اومد پرایوت کی و vps ip تون رو بزنید

تو این مرحله rpc رو باید جایگذاری باید کنید بعد این عبارت --eth-rpc-url  نوشته  your   rpc  جایگرین میکنید بعد سیو میکنید 

```
nano docker-compose.yaml
```

# ران کردن 
```
docker compose up -d
docker logs -f drosera-node
```

![image](https://github.com/user-attachments/assets/ae5a859e-d299-4ef3-93be-720b36daecf7)


# مرحله بعد  Opt-in to Trap
![image](https://github.com/user-attachments/assets/596044a7-202b-4685-b815-11d1d60953b1)



وآخر  وضعیت نودتون تو داشبورد باید اینطور باشه 

![image](https://github.com/user-attachments/assets/b1aee33b-43c6-4adc-b973-7ff3efe9b1db)



