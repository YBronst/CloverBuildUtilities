# Clover Update Script

This is clone of Python [https://github.com/hnanoto/Update_Clover] script automates the process of updating your Clover bootloader to the latest version available in the [https://github.com/YBronst/CloverBootloader] repository. It is designed to simplify and speed up the update process, making it more accessible to Hackintosh community users. https://www.youtube.com/channel/UC-SkAYQyY0e49ALoOrdcOTQ https://discord.gg/5hvZ5u7QXQ

## Features

- **Automatic Language Detection:** The script automatically detects the system language (Portuguese or English) and displays messages in the corresponding language.  
- **Interactive Menu:** Allows you to choose which components to update: **Update BOOTX64.efi and CLOVERX64.efi** updates only the main Clover boot files; **Update Drivers** updates only the UEFI drivers in the `EFI/CLOVER/Drivers/UEFI` folder; **Full Update** updates both boot files and UEFI drivers.  
- **Environment Check:** Ensures the script is running on macOS.  
- **Dependency Check:** Verifies that the necessary commands are available: `curl`, `unzip`, `/usr/libexec/PlistBuddy`, `installer`.  
- **Smart Download:** Downloads the latest Clover release only once and reuses it for all update operations, saving time and bandwidth.  
- **Bootloader Detection:** Checks if the selected EFI partition contains a Clover installation. If OpenCore or Windows Boot Manager is detected, the script aborts to prevent damage.  
- **Wait for Mount:** If the selected EFI partition is not mounted, the script waits until it is manually mounted and provides clear instructions.  
- **EFI Backup:** Creates a full backup of your EFI partition before making any changes. Backups are stored in the `EFI_BACKUPS` folder in the user's home directory, with names containing the date and time. If a backup already exists for the same minute, it is numbered sequentially.  
- **Safe Update:** Ensures the EFI partition is mounted as read/write before updating.  
- **Error Handling:** Captures errors and displays clear, informative messages. A custom exception `CloverUpdateError` is used for script-specific errors.  
- **Detailed Logging:** Generates a detailed log file `update_clover_[timestamp].log` in the same folder as the script, recording all actions, warnings, and errors.  
- **Cleanup:** Removes temporary downloaded files after the update is complete.  
- **Internationalization:** Supports messages in Portuguese (pt-BR) and English (en-US). Language is detected automatically based on system settings. Portuguese is used by default if detection fails or no corresponding translation file exists.

## Prerequisites

- **macOS:** Script is intended for macOS.  
- **Python 3:** Ensure Python 3 is installed (`python3 --version`).  
- **Python Modules:** Only standard Python library is used; **no additional packages via pip are required**.  
- **Dependencies:** The script relies on: `curl`, `unzip`, `/usr/libexec/PlistBuddy`, `installer` (usually preinstalled).  
- **Internet Connection:** Required to download the latest Clover release.  
- **Mounted EFI Partition:** The EFI partition to be updated must be mounted and writable. Mount manually if needed: `diskutil mount <partition_identifier>` (example: `diskutil mount disk0s1`).

## How to Run

1. **Download the script:** `main.py` and the files `clover_updater.py`, `config.py`, `efi_handler.py`, `logger.py`, `menu.py`, `utils.py`, and the `translations` folder.  
2. **Unzip and place all files in the same folder**, e.g., `update_clover`.  
3. **Make the script executable:** `cd update_clover` then `chmod +x main.py`.  
4. **Run with administrator privileges:** `sudo python3 main.py`.  
5. **Follow on-screen instructions:** Select the EFI partition to update, ensure it is mounted, script will create a backup and display update options, choose an option and press Enter, monitor progress via terminal output and `update_clover_[timestamp].log`.

## Interactive Menu

1. **Update BOOTX64.efi and CLOVERX64.efi** – updates main Clover boot files.  
2. **Update Drivers** – updates UEFI drivers.  
3. **Full Update** – updates boot files and UEFI drivers.  
4. **Exit** – quits the script.

## Important Notes

- **Backup:** Although the script creates backups, it is recommended to manually backup EFI as an extra precaution.  
- **UEFI Drivers:** Script **only updates existing UEFI drivers**; it **does not add new drivers**. Ensure required drivers are already present.  
- **Modification Date:** Original modification dates of Clover files are preserved; updated files may appear to have future dates depending on the Clover release.  
- **Tested on:** macOS Ventura 13.6.3.

## Troubleshooting

- **Permission Errors:** Run with `sudo`.  
- **Download Failure:** Check internet connection.  
- **EFI Not Mounted:** Mount manually (`diskutil mount <partition_identifier>`).  
- **EFI Read-Only:** Unmount and remount; if the problem persists, investigate system-specific issues or ask Hackintosh community for help.

## Contributions

Contributions are welcome! Open a Pull Request with improvements.

## Credits

- **Clover Developers:** For the excellent Clover bootloader.  
- **Hackintosh Community:** For support and shared knowledge.  
- **Henrique/hnanoto:** For creating this script.

## Disclaimer

Provided "as-is," without warranty. Authors and contributors are not responsible for any damages. Use at your own risk. Always make a full system backup before modifications.

## Update: Automatic Language Detection

Script now supports translation of messages into different languages (Portuguese and English). Language is detected via `locale.getdefaultlocale()`. Loads corresponding JSON file from `translations` folder. Defaults to English if no translation for the system language is found.

# CloverAutoBuilder v5

# Purpose:
- Fully rebuilds the CloverBootloader repository.
- preserving files in toolchain/tools/download to avoid re-downloading large archives
- (e.g., gcc-15.1.0.tar.xz).

# Usage:
  1. Make the script executable:
```bash
 chmod +x CloverAutoBuilder
```
  3. Remove from quarantine:
```bash
xattr -dr com.apple.quarantine CloverAutoBuilder
```
  5. Run the script:
```bash
./CloverAutoBuilder
```

# What it can do:
  - Checks for Python (installs if needed);
  - Creates a symlink for python if missing;
  - Updates pip and setuptools;
  - If CloverBootloader exists:
       * Saves toolchain/tools/download to /private/tmp/downloadBackup
       * Deletes the old repository
  - Clones a fresh CloverBootloader from GitHub;
  - Restores saved files back into toolchain/tools/download or downloads CloverBuildTools.zip if no backup exists;
  - Checks for all required build tools;
  - Builds BaseTools;
  - Automatically runs buildme;
  - Cleans up /private/tmp/downloadBackup after completion.

# CloverBuildTool By chris1111 
- Loads slowly loads open source tools that may have been lost during updates CloverBootloader

# Usage:
- Place it next to CloverBootloader and launch it and missing files will appear in `CloverBootloader/toolchain/tools/Download`
- The preparation is the same as for the previous tool.

# Differences:
- Does not remove or modify any files ni CloverBootloader

# MacFileHelper Quickly make scripts executable or remove quarantine from apps and installers on macOS.
## Features:

- Make scripts (`.sh`, `.py`, `.command`, or files with shebang) executable.
- Remove quarantine from apps (`.app`) and installers (`.dmg`, `.pkg`, `.zip`).
- Spinner animation and color-coded labels for easy feedback.
- Safe folder handling: only one candidate file is processed.
- Logs all actions to `~/Desktop/FileTool3.log`.

## Usage:

1. Make the script executable:

```bash
chmod +x "path to" MacFileHelper
```
  
# Homebrew (un)installer

## Install Homebrew (on macOS or Linux)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

More installation information and options: <https://docs.brew.sh/Installation>.

If you're on macOS, try out our new `.pkg` installer. Download it from [Homebrew's latest GitHub release](https://github.com/Homebrew/brew/releases/latest).

If you are running Linux or WSL, [there are some pre-requisite packages to install](https://docs.brew.sh/Homebrew-on-Linux#requirements).

You can set `HOMEBREW_NO_INSTALL_FROM_API` to tap Homebrew/homebrew-core; by default, it will not be tapped as it is no longer necessary.

You can set `HOMEBREW_BREW_GIT_REMOTE` and/or `HOMEBREW_CORE_GIT_REMOTE` in your shell environment to use geolocalized Git mirrors to speed up Homebrew's installation with this script and, after installation, `brew update`.

```bash
export HOMEBREW_BREW_GIT_REMOTE="..."  # put your Git mirror of Homebrew/brew here
export HOMEBREW_CORE_GIT_REMOTE="..."  # put your Git mirror of Homebrew/homebrew-core here
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

The default Git remote will be used if the corresponding environment variable is unset.

If you want to run the Homebrew installer non-interactively without prompting for passwords (e.g. in automation scripts), you can use:

```bash
NONINTERACTIVE=1 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## Uninstall Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/uninstall.sh)"
```

If you want to run the Homebrew uninstaller non-interactively, you can use:

```bash
NONINTERACTIVE=1 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/uninstall.sh)"
```

If you want to to uninstall Homebrew from a specific prefix (e.g. when migrating from Intel to Apple Silicon processors), download the uninstall script and run it with `--path`:

```
curl -fsSLO https://raw.githubusercontent.com/Homebrew/install/HEAD/uninstall.sh
/bin/bash uninstall.sh --path /usr/local
```

Run the downloaded script with `/bin/bash uninstall.sh --help` to view more uninstall options.
