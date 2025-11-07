# My Arch Linux Setup Guide.

## Arch Linux Installation Guide using `archinstall`

The `archinstall` script provides a streamlined, interactive, and menu-driven way to automate the installation of Arch Linux, eliminating the need for manual commands.

## Prerequisites

Before running the script, ensure you have the following:

1.  **Arch Linux ISO:** Download the latest ISO and create a bootable USB drive.
2.  **Boot:** Boot your target machine from the USB drive to enter the live environment.
3.  **Ensure Network Connectivity:**  
  * Wired: If you have a wired connection, you are usually connected automatically.

 * Wireless: If you are using Wi-Fi, you may need to connect using the **iwctl** utility before running archinstall.


## Running the archinstall Script

The **archinstall** script is included in the live environment.

  1. **Start the Script:**
  ```bash
  archinstall
  ```
2. **Follow the Prompts:**

    The script will guide you through the installation process with a series of menus and prompts. Key steps include:

    *   **Localization:** Select Language and Keyboard Layout.
    *   **Mirror Region:** Choose the closest mirror for faster downloads.
    *   **Disk Configuration:** Select your hard drive(s), disk layout (e.g., wipe and use default, custom partitioning), filesystem (e.g., Ext4).
    *   **Bootloader:** Select a bootloader (e.g.systemd-boot).
    *   **User Setup:** create a standard user account.
    *   **Profile/Desktop Environment:** Choose a Minimal profile.
    *   **Network Configuration:** Set up networking (e.g., NetworkManager).
    *   **Timezone:** Configure your geographic timezone.
    * **Install:** It will take some time. after installing reboot the system.

