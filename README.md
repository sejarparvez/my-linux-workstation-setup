# My Arch Linux Workstation Setup Guide

This repository provides a guide and configuration files for setting up an Arch Linux workstation. The primary focus is on automating the initial installation using `archinstall` and then configuring a minimal desktop environment with essential tools.

## 1. Arch Linux Installation using `archinstall`

The `archinstall` script offers a streamlined, interactive, and menu-driven approach to automate the installation of Arch Linux, significantly simplifying the process compared to manual installation.

### Prerequisites

Before proceeding with the `archinstall` script, ensure you have completed the following steps:

1.  **Arch Linux ISO:** Download the latest Arch Linux ISO image and create a bootable USB drive.
2.  **Boot from USB:** Boot your target machine from the prepared USB drive to enter the Arch Linux live environment.
3.  **Network Connectivity:** Verify that you have an active internet connection.
    *   **Wired Connection:** Typically, a wired connection is established automatically.
    *   **Wireless Connection:** If using Wi-Fi, you may need to connect manually using the `iwctl` utility within the live environment before running `archinstall`.

### Running the `archinstall` Script

The `archinstall` script is readily available in the live environment.

1.  **Start the Script:**
    Open a terminal in the live environment and execute:
    ```bash
    archinstall
    ```
2.  **Follow the Interactive Prompts:**
    The script will guide you through the installation process with a series of interactive menus and prompts. Key configuration steps include:

    *   **Localization:** Select your preferred language and keyboard layout.
    *   **Mirror Region:** Choose the geographically closest mirror for optimized download speeds.
    *   **Disk Configuration:** Define your storage setup. Options typically include:
        *   Wipe and use default partitioning.
        *   Custom partitioning.
        *   Selection of filesystem (e.g., Ext4, Btrfs).
    *   **Bootloader:** Select a bootloader (e.g., `systemd-boot`, GRUB).
    *   **User Setup:** Create a standard user account with sudo privileges.
    *   **Profile/Desktop Environment:** For a minimal setup, choose the "Minimal" profile.
    *   **Network Configuration:** Configure networking services (e.g., NetworkManager).
    *   **Timezone:** Set your geographic timezone.
    *   **Initiate Installation:** Once all selections are made, confirm to start the installation process. This will take some time.

3.  **Reboot System:**
    After the installation completes successfully, reboot your system into the newly installed Arch Linux.

## 2. Post-Installation Setup

After successfully installing Arch Linux, follow these steps to set up your workstation:

### 2.1 Install Essential Packages

First, update your system and install essential development tools and utilities:

```bash
sudo pacman -Syu
sudo pacman -S fish git wget curl gcc make cmake nano neovim
```

### 2.2 Install Caelestia Shell Configuration

Clone the Caelestia shell configuration repository and run its installation script:

```bash
git clone https://github.com/caelestia-dots/caelestia.git ~/.local/share/caelestia
~/.local/share/caelestia/install.fish
```

### 2.3 Install and Enable SDDM

SDDM is a modern display manager for X11 and Wayland.

1.  Install SDDM:
    ```bash
    sudo pacman -S sddm
    ```
2.  Enable and start SDDM:
    ```bash
    sudo systemctl enable sddm
    sudo systemctl start sddm
    ```

Now reboot the system to apply all the changes.

## 3. Wallpapers and SDDM Theme

#### 3.1 Wallpapers

1.  **Clone Wallpapers:**
    ```bash
    git clone https://github.com/linuxforwork/wallpaper.git ~/Pictures/Wallpapers
    ```
    *Note: The repository name was corrected to `mylinuxforwork-wallpapers.git` and the URL to `https://github.com`.*

####  3.2 SDDM Theme (Sugar Candy)

1.  **Install Sugar Candy Theme:**
    ```bash
    paru -S sddm-sugar-candy
    ```
    *Note: This command requires root privileges.*

2.  **Set SDDM Theme:**
    Edit the SDDM configuration file to set the `sugar-candy` theme.
    ```bash
    sudo nvim /usr/lib/sddm/sddm.conf.d/default.conf
    ```
    Add or modify the `[Theme]` section to include:
    ```
    [Theme]
    Current=Sugar-Candy
    ```
    Save and exit the editor.

3.  **Apply Changes:**
    Reboot your system for the changes to take effect.
    ```bash
    sudo reboot
    ```

## 4. Essential Apps

Install essential applications. Some are available in the official Arch repositories via `pacman`, while others require an AUR helper like `paru`.

### 4.1 Install Pacman Packages

```bash
sudo pacman -S --needed thunar kdeconnect thunderbird ark
```

### 4.2 Install AUR Packages (using paru)

```bash
paru -S --needed zen-browser-bin visual-studio-code-bin spotify brave-bin
```