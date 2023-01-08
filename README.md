# Install wifi driver
Make sure you hava a internet connection. now paste the following code in terminal.

```

sudo apt-get install build-essential git dkms linux-headers-$(uname -r)

```
```
git clone https://github.com/McMCCRU/rtl8188gu.git

```
```
cd rtl8188gu

```
```
make

```
```
sudo make install

```
```
sudo apt install --reinstall linux-firmware

```
```
sudo reboot

```


# Install NodeJs

01. Download NodeJs binary for linux mint / Ubuntu / Debian

02. Go to Downloads folder 📂 find the .tar file and extract it.

03. Now Open Terminal in the newly created directory and paste the following Commend in terminal..

```

sudo cp -r ./{lib,share,include,bin} /usr


```


# Install VS Code

Download The .deb file from official visual studio code website. Than install it..

# Install mongodb

```
wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | apt-key add -

```
```
echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-4.2.list
```
```
apt update
```
```
apt install mongodb -y
```
```
systemctl start mongodb
```
```
systemctl enable mongodb
```
```
mongo
```
