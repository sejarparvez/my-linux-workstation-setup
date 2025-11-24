# My Arch Linux Workstation Setup

This repository contains all the necessary configuration files and a comprehensive guide to setting up a personalized Arch Linux workstation from scratch. The setup is designed to be efficient, starting with an automated installation using `archinstall` and culminating in a sleek, minimal desktop environment.

## Table of Contents
- [My Arch Linux Workstation Setup](#my-arch-linux-workstation-setup)
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
    - [3.4 Fix Weather and temperature unit.](#34-fix-weather-and-temperature-unit)
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
    *   **Disk Configuration:** Use the option to wipe the drive and use a default partition layout with the **Ext4** filesystem.
    *   **Bootloader:** The default, `systemd-boot`, is a good choice.
    *   **Profile:** Select the **"Minimal"** profile.
    *   **User:** Create a user and grant it superuser (sudo) privileges.
    *   **Network:** Use **NetworkManager**.

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

### 3.4 Fix Weather and temperature unit.

```bash
nvim ~/.config/caelestia/shell.json
```
```bash
{
  "general": {
    "idle": {
      "lockBeforeSleep": true,
      "inhibitWhenAudio": true,
      "timeouts": [
        {
          "timeout": 600,
          "idleAction": "lock"
        },
        {
          "timeout": 1800,
          "idleAction": "dpms off",
          "returnAction": "dpms on"
        },
        {
          "timeout": 3600,
          "idleAction": [
            "systemctl",
            "suspend-then-hibernate"
          ]
        }
      ]
    }
  },
  "background": {
    "desktopClock": {
      "enabled": true
    },
    "enabled": true
  },
  "bar": {
    "clock": {
      "showIcon": false
    },
    "persistent": false,
    "scrollActions": {
      "brightness": true,
      "workspaces": true,
      "volume": true
    },
    "showOnHover": true,
    "status": {
      "showAudio": true,
      "showBattery": false,
      "showBluetooth": false,
      "showLockStatus": false
    }
  },
  "border": {
    "rounding": 10,
    "thickness": 1.5
  },
  "dashboard": {
    "showOnHover": false
  },
  "osd": {
    "enabled": false
  },
  "services": {
    "weatherLocation": "23.54,89.18",
    "useFahrenheit": false,
    "useTwelveHourClock": true
  },
  "utilities": {
    "toasts": {
      "capsLockChanged": false
    }
  }
}

```

## 4. Essential Applications

### 4.1 Install Pacman Packages

```bash
sudo pacman -S --needed thunar kdeconnect thunderbird ark gvfs tumbler qimgv
```

### 4.2 Install AUR Packages

```bash
paru -S --needed zen-browser-bin visual-studio-code-bin spotify brave-bin mongodb-compass-bin
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
    *A warning about VS Code being "corrupted" is expected. This is normal when applying custom styles and can be dismissed.*

### 5.2 Essential Extensions

-   **Auto Close Tag**
-   **Auto Rename Tag**
-   **Biome**
-   **Catppuccin for VS Code**
-   **Code Spell Checker**
-   **Markdown All in One**
-   **Material Icon Theme**
-   **Tailwind CSS IntelliSense**
-   **Thunder Client**
-   **Toggle Excluded Files**
-   **Windsurf Plugin**

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