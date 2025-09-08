================ CloverAutoBuilder v5 =================
Purpose:
  Fully rebuilds the CloverBootloader repository while
  preserving files in toolchain/tools/download to avoid
  re-downloading large archives (e.g., gcc-15.1.0.tar.xz).

Usage:
  1. Make the script executable:
       chmod +x CloverAutoBuilder
  2. Remove from macOS quarantine
       sudo xattr -rd com.apple.quarantine 
  3. Run the script:
       ./CloverAutoBuilder

What it does:
  - Checks for Python (installs if needed)
  - Creates a symlink for python if missing
  - Updates pip and setuptools
  - If CloverBootloader exists:
       * Saves toolchain/tools/download to /private/tmp/downloadBackup
       * Deletes the old repository
  - Clones a fresh CloverBootloader from GitHub
  - Restores saved files back into toolchain/tools/download
    OR downloads CloverBuildTools.zip if no backup exists
  - Checks for all required build tools
  - Builds BaseTools
  - Automatically runs buildme
  - Cleans up /private/tmp/downloadBackup after completion
