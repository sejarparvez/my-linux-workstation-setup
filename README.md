# My Linux Workstation Setup

This repository contains all the necessary configuration files and a comprehensive guide to setting up a personalized Arch Linux workstation from scratch. The setup is designed to be efficient, starting with an automated installation using `archinstall` and culminating in a sleek, minimal desktop environment.

## Table of Contents

- [My Linux Workstation Setup](#my-linux-workstation-setup)
  - [Table of Contents](#table-of-contents)
  - [1. Arch Linux Installation with `archinstall`](#1-arch-linux-installation-with-archinstall)
    - [Prerequisites](#prerequisites)
    - [Running the Installer](#running-the-installer)
  - [2. Essential Post-Installation Setup](#2-essential-post-installation-setup)
    - [2.1 Update System and Install Git](#21-update-system-and-install-git)
    - [2.2 Install an AUR Helper (Paru)](#22-install-an-aur-helper-paru)
    - [2.3 Install Caelestia Shell Configuration](#23-install-caelestia-shell-configuration)
  - [3. Setting Up the Desktop Environment](#3-setting-up-the-desktop-environment)
    - [3.1 Install and Enable SDDM](#31-install-and-enable-sddm)
    - [3.2 Download Wallpapers](#32-download-wallpapers)
    - [3.3 Configure SDDM Theme (Sugar Candy)](#33-configure-sddm-theme-sugar-candy)
    - [3.4 Add our custom user config.](#34-add-our-custom-user-config)
  - [4. Essential Applications](#4-essential-applications)
    - [4.1 Install Pacman Packages](#41-install-pacman-packages)
    - [4.2 Install AUR Packages](#42-install-aur-packages)
  - [5. VS Code Customizations](#5-vs-code-customizations)
    - [5.1 Applying Customizations](#51-applying-customizations)
    - [5.2 Essential Extensions](#52-essential-extensions)
  - [6. More Applications and Tools](#6-more-applications-and-tools)
    - [6.1 Fonts](#61-fonts)
    - [6.2 Node.js, npm, pnpm, and Biome](#62-nodejs-npm-pnpm-and-biome)

## 1. Arch Linux Installation with `archinstall`

The `archinstall` script provides a guided, menu-driven installation of Arch Linux, making the process much simpler than a manual setup.

### Prerequisites

1.  **Arch Linux ISO:** [Download the latest ISO](https://archlinux.org/download/) and create a bootable USB drive.
2.  **Boot:** Boot your machine from the USB drive.
3.  **Network:** Ensure you have a working internet connection. For Wi-Fi, use the `iwctl` utility in the live environment to connect.

### Running the Installer

1.  **Launch the script:**
    ```bash
    archinstall
    ```
2.  **Follow the prompts:** The script will guide you through the setup. Below are some recommendations for a minimal setup:
    - **Disk Configuration:** Use the option to wipe the drive and use a default partition layout with the **BTRFS** filesystem.
    - **Bootloader:** The default, `systemd-boot`, is a good choice.
    - **Profile:** Select the **"Minimal"** profile.
    - **User:** Create a user and grant it superuser (sudo) privileges.
    - **Network:** Use **NetworkManager**.

3.  **Reboot:** After the installation is complete, reboot your system.

## 2. Essential Post-Installation Setup

### 2.1 Update System and Install Git

After rebooting into your new system, open a terminal and run the following command to update your package manager and install `git`:

```bash
sudo pacman -Syu git
```

### 2.2 Install an AUR Helper (Paru)

The Arch User Repository (AUR) contains a vast collection of community-maintained packages. `paru` is an AUR helper that makes it easy to install and manage these packages.

```bash
sudo pacman -S --needed base-devel
git clone https://aur.archlinux.org/paru.git
cd paru && makepkg -si && cd .. && rm -rf paru
```

### 2.3 Install Caelestia Shell Configuration

This will set up a beautiful and functional shell environment.

```bash
git clone https://github.com/caelestia-dots/caelestia.git ~/.local/share/caelestia
~/.local/share/caelestia/install.fish
```

After this, reboot your system to apply the shell changes.

## 3. Setting Up the Desktop Environment

### 3.1 Install and Enable SDDM

SDDM is a modern and lightweight display manager.

1.  **Install SDDM:**
    ```bash
    sudo pacman -S sddm
    ```
2.  **Enable SDDM:** This will make SDDM start automatically on boot.
    ```bash
    sudo systemctl enable sddm
    ```

### 3.2 Download Wallpapers

1.  **Clone the wallpapers repository:**
    ```bash
    git clone https://github.com/mylinuxforwork/wallpaper.git ~/Pictures/Wallpapers
    ```
2.  **Set a wallpaper (optional):** You can set a desktop wallpaper now or after the final reboot.
    - Press the **Super** key to open the application launcher.
    - Type `>` to enter command mode.
    - Select "Wallpaper" from the dropdown and choose your desired wallpaper.

### 3.3 Configure SDDM Theme (Sugar Candy)

1.  **Install the theme:**
    ```bash
    paru -S sddm-sugar-candy
    ```
2.  **Set the theme:**
    Create or edit the SDDM configuration file:
    ```bash
    sudo nvim /usr/lib/sddm/sddm.conf.d/default.conf
    ```
    Add the following content:
    ```ini
    [Theme]
    Current=sugar-candy
    ```
3.  **Set the lock screen background:**
    Copy a wallpaper to the theme's background directory.
    ```bash
    sudo cp ~/Pictures/Wallpapers/emergence.jpg /usr/share/sddm/themes/sugar-candy/Backgrounds/
    ```
    Then, update the theme configuration to use the new background:
    ```bash
    sudo nvim /usr/share/sddm/themes/sugar-candy/theme.conf
    ```
    Change the `Background` property to:
    ```ini
    Background="Backgrounds/emergence.jpg"
    ```
4.  **Reboot** to see all the desktop environment changes.
    ```bash
    sudo reboot
    ```

### 3.4 Add our custom user config.

```bash
nvim ~/.config/caelestia/shell.json
```
<details><summary><code>shell.json</code></summary>

```bash
{
  "appearance": {
    "rounding": {
      "scale": 1
    },
    "spacing": {
      "scale": 1
    },
    "padding": {
      "scale": 1
    },
    "font": {
      "family": {
        "sans": "Rubik",
        "mono": "CaskaydiaCove NF",
        "material": "Material Symbols Rounded",
        "clock": "Rubik"
      },
      "size": {
        "scale": 1
      }
    },
    "anim": {
      "durations": {
        "scale": 1
      }
    },
    "transparency": {
      "enabled": false,
      "base": 0.85,
      "layers": 0.4
    }
  },
  "general": {
    "logo": "",
    "apps": {
      "terminal": [
        "foot"
      ],
      "audio": [
        "pavucontrol"
      ],
      "playback": [
        "mpv"
      ],
      "explorer": [
        "thunar"
      ]
    },
    "idle": {
      "lockBeforeSleep": true,
      "inhibitWhenAudio": true,
      "timeouts": [
        {
          "idleAction": "lock",
          "timeout": 600
        },
        {
          "idleAction": "dpms off",
          "returnAction": "dpms on",
          "timeout": 1800
        },
        {
          "idleAction": [
            "systemctl",
            "suspend-then-hibernate"
          ],
          "timeout": 3600
        }
      ]
    },
    "battery": {
      "warnLevels": [
        {
          "icon": "battery_android_frame_2",
          "level": 20,
          "message": "You might want to plug in a charger",
          "title": "Low battery"
        },
        {
          "icon": "battery_android_frame_1",
          "level": 10,
          "message": "You should probably plug in a charger <b>now</b>",
          "title": "Did you see the previous message?"
        },
        {
          "critical": true,
          "icon": "battery_android_alert",
          "level": 5,
          "message": "PLUG THE CHARGER RIGHT NOW!!",
          "title": "Critical battery level"
        }
      ],
      "criticalLevel": 3
    }
  },
  "background": {
    "enabled": true,
    "desktopClock": {
      "enabled": true
    },
    "visualiser": {
      "enabled": true,
      "autoHide": true,
      "blur": true,
      "rounding": 1,
      "spacing": 1
    }
  },
  "bar": {
    "persistent": false,
    "showOnHover": true,
    "dragThreshold": 20,
    "scrollActions": {
      "workspaces": true,
      "volume": true,
      "brightness": true
    },
    "popouts": {
      "activeWindow": false,
      "tray": true,
      "statusIcons": true
    },
    "workspaces": {
      "shown": 4,
      "activeIndicator": true,
      "occupiedBg": false,
      "showWindows": false,
      "showWindowsOnSpecialWorkspaces": false,
      "activeTrail": false,
      "perMonitorWorkspaces": true,
      "label": "  ",
      "occupiedLabel": "󰮯",
      "activeLabel": "󰮯",
      "capitalisation": "preserve",
      "specialWorkspaceIcons": []
    },
    "tray": {
      "background": false,
      "recolour": false,
      "compact": false,
      "iconSubs": []
    },
    "status": {
      "showAudio": true,
      "showMicrophone": false,
      "showKbLayout": false,
      "showNetwork": true,
      "showWifi": true,
      "showBluetooth": false,
      "showBattery": false,
      "showLockStatus": false
    },
    "clock": {
      "showIcon": false
    },
    "sizes": {
      "innerWidth": 40,
      "windowPreviewSize": 400,
      "trayMenuWidth": 300,
      "batteryWidth": 250,
      "networkWidth": 320
    },
    "entries": [
      {
        "enabled": true,
        "id": "logo"
      },
      {
        "enabled": true,
        "id": "workspaces"
      },
      {
        "enabled": true,
        "id": "spacer"
      },
      {
        "enabled": true,
        "id": "activeWindow"
      },
      {
        "enabled": true,
        "id": "spacer"
      },
      {
        "enabled": true,
        "id": "tray"
      },
      {
        "enabled": true,
        "id": "clock"
      },
      {
        "enabled": true,
        "id": "statusIcons"
      },
      {
        "enabled": true,
        "id": "power"
      }
    ]
  },
  "border": {
    "thickness": 1.5,
    "rounding": 10
  },
  "dashboard": {
    "enabled": true,
    "showOnHover": false,
    "mediaUpdateInterval": 500,
    "dragThreshold": 50,
    "sizes": {
      "tabIndicatorHeight": 3,
      "tabIndicatorSpacing": 5,
      "infoWidth": 200,
      "infoIconSize": 25,
      "dateTimeWidth": 110,
      "mediaWidth": 200,
      "mediaProgressSweep": 180,
      "mediaProgressThickness": 8,
      "resourceProgessThickness": 10,
      "weatherWidth": 250,
      "mediaCoverArtSize": 150,
      "mediaVisualiserSize": 80,
      "resourceSize": 200
    }
  },
  "controlCenter": {
    "sizes": {
      "heightMult": 0.7,
      "ratio": 1.7777777777777777
    }
  },
  "launcher": {
    "enabled": true,
    "showOnHover": false,
    "maxShown": 7,
    "maxWallpapers": 9,
    "specialPrefix": "@",
    "actionPrefix": ">",
    "enableDangerousActions": false,
    "dragThreshold": 50,
    "vimKeybinds": false,
    "hiddenApps": [
      "lstopo",
      "thunar-settings",
      "avahi-discover",
      "xfce4-about",
      "bssh",
      "bvnc",
      "thunar-bulk-rename",
      "cmake-gui",
      "footclient",
      "foot-server",
      "org.kde.kdeconnect.nonplasma",
      "org.kde.kdeconnect.sms",
      "assistant",
      "qdbusviewer",
      "linguist",
      "designer",
      "qt6ct",
      "qv4l2",
      "qvidcap",
      "qt5ct"
    ],
    "useFuzzy": {
      "apps": false,
      "actions": false,
      "schemes": false,
      "variants": false,
      "wallpapers": false
    },
    "sizes": {
      "itemWidth": 600,
      "itemHeight": 57,
      "wallpaperWidth": 280,
      "wallpaperHeight": 200
    },
    "actions": [
      {
        "command": [
          "autocomplete",
          "calc"
        ],
        "dangerous": false,
        "description": "Do simple math equations (powered by Qalc)",
        "enabled": true,
        "icon": "calculate",
        "name": "Calculator"
      },
      {
        "command": [
          "autocomplete",
          "scheme"
        ],
        "dangerous": false,
        "description": "Change the current colour scheme",
        "enabled": true,
        "icon": "palette",
        "name": "Scheme"
      },
      {
        "command": [
          "autocomplete",
          "wallpaper"
        ],
        "dangerous": false,
        "description": "Change the current wallpaper",
        "enabled": true,
        "icon": "image",
        "name": "Wallpaper"
      },
      {
        "command": [
          "autocomplete",
          "variant"
        ],
        "dangerous": false,
        "description": "Change the current scheme variant",
        "enabled": true,
        "icon": "colors",
        "name": "Variant"
      },
      {
        "command": [
          "autocomplete",
          "transparency"
        ],
        "dangerous": false,
        "description": "Change shell transparency",
        "enabled": false,
        "icon": "opacity",
        "name": "Transparency"
      },
      {
        "command": [
          "caelestia",
          "wallpaper",
          "-r"
        ],
        "dangerous": false,
        "description": "Switch to a random wallpaper",
        "enabled": true,
        "icon": "casino",
        "name": "Random"
      },
      {
        "command": [
          "setMode",
          "light"
        ],
        "dangerous": false,
        "description": "Change the scheme to light mode",
        "enabled": true,
        "icon": "light_mode",
        "name": "Light"
      },
      {
        "command": [
          "setMode",
          "dark"
        ],
        "dangerous": false,
        "description": "Change the scheme to dark mode",
        "enabled": true,
        "icon": "dark_mode",
        "name": "Dark"
      },
      {
        "command": [
          "systemctl",
          "poweroff"
        ],
        "dangerous": true,
        "description": "Shutdown the system",
        "enabled": true,
        "icon": "power_settings_new",
        "name": "Shutdown"
      },
      {
        "command": [
          "systemctl",
          "reboot"
        ],
        "dangerous": true,
        "description": "Reboot the system",
        "enabled": true,
        "icon": "cached",
        "name": "Reboot"
      },
      {
        "command": [
          "loginctl",
          "terminate-user",
          ""
        ],
        "dangerous": true,
        "description": "Log out of the current session",
        "enabled": true,
        "icon": "exit_to_app",
        "name": "Logout"
      },
      {
        "command": [
          "loginctl",
          "lock-session"
        ],
        "dangerous": false,
        "description": "Lock the current session",
        "enabled": true,
        "icon": "lock",
        "name": "Lock"
      },
      {
        "command": [
          "systemctl",
          "suspend-then-hibernate"
        ],
        "dangerous": false,
        "description": "Suspend then hibernate",
        "enabled": true,
        "icon": "bedtime",
        "name": "Sleep"
      },
      {
        "command": [
          "caelestia",
          "shell",
          "controlCenter",
          "open"
        ],
        "dangerous": false,
        "description": "Configure the shell",
        "enabled": true,
        "icon": "settings",
        "name": "Settings"
      }
    ]
  },
  "notifs": {
    "expire": true,
    "defaultExpireTimeout": 5000,
    "clearThreshold": 0.3,
    "expandThreshold": 20,
    "actionOnClick": false,
    "groupPreviewNum": 3,
    "sizes": {
      "width": 400,
      "image": 41,
      "badge": 20
    }
  },
  "osd": {
    "enabled": false,
    "hideDelay": 2000,
    "enableBrightness": true,
    "enableMicrophone": false,
    "sizes": {
      "sliderWidth": 30,
      "sliderHeight": 150
    }
  },
  "session": {
    "enabled": true,
    "dragThreshold": 30,
    "vimKeybinds": false,
    "commands": {
      "logout": [
        "loginctl",
        "terminate-user",
        ""
      ],
      "shutdown": [
        "systemctl",
        "poweroff"
      ],
      "hibernate": [
        "systemctl",
        "hibernate"
      ],
      "reboot": [
        "systemctl",
        "reboot"
      ]
    },
    "sizes": {
      "button": 80
    }
  },
  "winfo": {
    "sizes": {
      "heightMult": 0.7,
      "detailsWidth": 500
    }
  },
  "lock": {
    "recolourLogo": false,
    "enableFprint": true,
    "maxFprintTries": 3,
    "sizes": {
      "heightMult": 0.7,
      "ratio": 1.7777777777777777,
      "centerWidth": 600
    }
  },
  "utilities": {
    "enabled": false,
    "maxToasts": 4,
    "sizes": {
      "width": 430,
      "toastWidth": 430
    },
    "toasts": {
      "configLoaded": true,
      "chargingChanged": true,
      "gameModeChanged": true,
      "dndChanged": true,
      "audioOutputChanged": true,
      "audioInputChanged": true,
      "capsLockChanged": false,
      "numLockChanged": false,
      "kbLayoutChanged": true,
      "vpnChanged": true,
      "nowPlaying": false
    },
    "vpn": {
      "enabled": false,
      "provider": [
        "netbird"
      ]
    }
  },
  "sidebar": {
    "enabled": true,
    "dragThreshold": 80,
    "sizes": {
      "width": 430
    }
  },
  "services": {
    "weatherLocation": "23.54,89.18",
    "useFahrenheit": false,
    "useTwelveHourClock": true,
    "gpuType": "",
    "visualiserBars": 45,
    "audioIncrement": 0.1,
    "maxVolume": 1,
    "smartScheme": true,
    "defaultPlayer": "Spotify",
    "playerAliases": [
      {
        "from": "com.github.th_ch.youtube_music",
        "to": "YT Music"
      }
    ]
  },
  "paths": {
    "wallpaperDir": "/home/sejar/Pictures/Wallpapers",
    "sessionGif": "root:/assets/kurukuru.gif",
    "mediaGif": "root:/assets/bongocat.gif"
  }
}


```

</details>

```bash
nvim ~/.config/caelestia/hypr-user.conf
```

<details> <summary><code>hypr-user.conf</code></summary>

``` bash
# Brightness
bindl = Ctrl+Super, F3, global, caelestia:brightnessUp
bindl = Ctrl+Super, F2, global, caelestia:brightnessDown


# Media
bindl = , F8, global, caelestia:mediaToggle
bindl = , F6, global, caelestia:mediaNext
bindl = , F5, global, caelestia:mediaPrev

# Apps
bind = Super, B, exec, app2unit -- brave
bind = Super, F1, exec, app2unit -- spotify-launcher
bind = Super+Shift, Z, exec, app2unit -- zeditor


# Volume
bindl = , F4, exec, wpctl set-mute @DEFAULT_AUDIO_SOURCE@ toggle
bindle = Super, F3, exec, wpctl set-mute @DEFAULT_AUDIO_SINK@ 0; wpctl set-volume -l 1 @DEFAULT_AUDIO_SINK@ $volumeStep%+
bindle = Super, F2, exec, wpctl set-mute @DEFAULT_AUDIO_SINK@ 0; wpctl set-volume @DEFAULT_AUDIO_SINK@ $volumeStep%-

exec-once = gnome-keyring-daemon --start --components=secrets
exec-once = dbus-update-activation-environment --systemd WAYLAND_DISPLAY XDG_CURRENT_DESKTOP


```
</details>

```bash
nvim ~/.config/caelestia/hypr-vars.conf
```

<details> <summary><code>hypr-vars.conf</code></summary>

``` bash
$editor = code

# Gaps
$workspaceGaps = 2
$windowGapsIn = 2
$windowGapsOut = 0
$singleWindowGapsOut = 0


$windowBorderSize = 2


```

</details>

## 4. Essential Applications

### 4.1 Install Pacman Packages

```bash
sudo pacman -S --needed thunar kdeconnect ark gvfs tumbler
```

### 4.2 Install AUR Packages

```**bash**
paru -S --needed zen-browser-bin visual-studio-code-bin spotify brave-bin mongodb-compass-bin qimgv
```

## 5. VS Code Customizations

This setup uses the **Custom CSS and JS Loader** extension to apply custom styles and scripts to VS Code.

### 5.1 Applying Customizations

1.  **Install the Extension:**
    Install the "[Custom CSS and JS Loader](https://marketplace.visualstudio.com/items?itemName=be5invis.vscode-custom-css)" extension by `be5invis` from the VS Code Marketplace.

2.  **Configure `settings.json`:**
    Add the following to your VS Code `settings.json` file. You can open it by pressing `Ctrl+Shift+P` and searching for "Preferences: Open User Settings (JSON)".

    ```json
    "vscode_custom_css.imports": [
        "file://${env:HOME}/MyCode/my-linux-workstation-setup/vscode-customizations/vscode-custom-css.css",
        "file://${env:HOME}/MyCode/my-linux-workstation-setup/vscode-customizations/vscode-custom-js.js"
    ],
    ```

    **Note:** The path `MyCode/my-linux-workstation-setup` assumes you've cloned this repository into a `MyCode` directory in your home folder. Please adjust the path if you've placed it elsewhere.

3.  **Enable Customizations:**
    From the VS Code Command Palette (`Ctrl+Shift+P`), run the command **"Enable Custom CSS and JS"**. You will need to restart VS Code for the changes to take effect.

4.  If you encounter a permissions error, run the following command and then try Step 3 again:
    ```bash
    sudo chown -R $(whoami) /opt/visual-studio-code
    ```
    _A warning about VS Code being "corrupted" is expected. This is normal when applying custom styles and can be dismissed._

### 5.2 Essential Extensions

- **Auto Close Tag**
- **Auto Rename Tag**
- **Biome**
- **Catppuccin for VS Code**
- **Code Spell Checker**
- **Markdown All in One**
- **Material Icon Theme**
- **Tailwind CSS IntelliSense**
- **Thunder Client**
- **Toggle Excluded Files**
- **Windsurf Plugin**

## 6. More Applications and Tools

### 6.1 Fonts

Install essential developer fonts:

```bash
sudo pacman -S ttf-fira-code
paru -S ttf-jetbrains-mono otf-geist-mono-nerd
```

### 6.2 Node.js, npm, pnpm, and Biome

Install JavaScript development tools:

```bash
sudo pacman -S nodejs npm
sudo pacman -S pnpm
sudo pacman -S biome
```
