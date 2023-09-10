# My Linux Mint 20.3 Setup guide.

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
sudo reboot

```

# Install NodeJs

1.  Download NodeJs binary for linux mint / Ubuntu / Debian

2.  Go to Downloads folder 📂 find the .tar file and extract it.

3.  Now Open Terminal in the newly created directory and paste the following Commend in terminal..

```

sudo cp -r ./{lib,share,include,bin} /usr


```

# Install mongodb Server

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

# Install Mongodb compass

you can can install mongodb compass from its official website.

# Install and setup Neovim

Install the letest version of neovim and configure it using Lazy vim

switch to the neovim-setup branch to get the config file.

# VS code setup

Switch to the vs-code-setup branch to see the process.

# Install Fish.

Install the fish shell and make it default shell.

### Install the oh my fish framwork.

```
curl -L https://get.oh-my.fish | fish
```

### Choose and Install a Theme

```
omf theme
```

```
omf instal cyan

```

```
omf theme cyan

```

### Fish Config

~/.config/fish/config.fish

```
if status is-interactive

    # Display a colorful custom greeting message with ASCII art
    echo -e "\e[1;36m SEJAR PARVEZ \e[0m"



    # Custom function to navigate to a specific directory
    function primetech
        cd ~/MyCode/PrimeTech/
    end

    # Alias for 'ls -l'
    alias ll "ls -l"

    # Alias for 'vim' to open Neovim
    alias vim nvim

end

```

# Install Kitty Terminal.

Install the letest version of kitty terminal and make it default terminal.

Set jetbarin mono as the terminal font.

### kitty config

~/.config/kitty/kitty.conf

```
#font
font_family      JetBrains Mono
bold_font        auto
italic_font      auto
bold_italic_font auto
bold_font        auto
italic_font      auto
bold_italic_font auto

tab_bar_min_tabs            1
tab_bar_edge                bottom
tab_bar_style               powerline
tab_powerline_style         slanted
tab_title_template          {title}{' :{}:'.format(num_windows) if num_windows > 1 else ''}

background_opacity 0.7

# The basic colors
foreground              #CDD6F4
background              #292C3E
selection_foreground    #292C3E
selection_background    #F5E0DC

# Cursor colors
cursor                  #27EAC0
cursor_text_color       #292C3E

# URL underline color when hovering with mouse
url_color               #F5E0DC

# Kitty window border colors
active_border_color     #FB04EC
inactive_border_color   #6C7086
bell_border_color       #F9E2AF

# OS Window titlebar colors
wayland_titlebar_color system
macos_titlebar_color   system

# Tab bar colors
active_tab_foreground   #292C3E
active_tab_background   #27EAC0
inactive_tab_foreground #CDD6F4
inactive_tab_background #1E1E2E
tab_bar_background      #292C3E

# Colors for marks (marked text in the terminal)
mark1_foreground #292C3E
mark1_background #B4BEFE
mark2_foreground #292C3E
mark2_background #CBA6F7
mark3_foreground #292C3E
mark3_background #74C7EC

# The 16 terminal colors

# black
color0 #45475A
color8 #585B70

# red
color1 #F38BA8
color9 #F38BA8

# green
color2  #CCDAE1
color10 #A6E3A1

# yellow
color3  #F9E2AF
color11 #F9E2AF

# blue
color4  #89B4FA
color12 #89B4FA

# magenta
color5  #F5C2E7
color13 #F5C2E7

# cyan
color6  #94E2D5
color14 #94E2D5

# white
color7  #BAC2DE
color15 #A6ADC8


```
