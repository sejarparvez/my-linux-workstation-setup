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
