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

# CloverBuildTools By chris1111 
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
