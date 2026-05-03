# upm
Unified Package Manager for Linux

upm is a lightweight, cross-distro wrapper for Linux package managers. It provides a unified syntax for installing, removing, updating, and searching packages across different Linux distributions, so you never have to remember whether it's apt, dnf, pacman, or zypper again.
Whether you're switching distros, managing multiple systems, or just tired of Googling package manager commands, upm has you covered.
✨ Features

✅ Unified Syntax – Use the same commands (install, remove, update, search) across all supported distros.

✅ Distro Detection – Automatically detects your Linux distribution and uses the correct package manager.

✅ Simple & Fast – No dependencies, just a single bash script.

✅ Config Support – Restore your packages from a config file after a fresh install.

✅ Extensible – Easy to add support for new distros or package managers.

📋 Supported Distros & Package Managers

Distro  Package Manager  Supported Actions
Ubuntu        apt        install, remove, update, search
Debian        apt        install, remove, update, search
Fedora        dnf        install, remove, update, search 
RHEL/CentOS   dnf        install, remove, update, search
Arch Linux   pacman      install, remove, update, search
Manjaro      pacman      install, remove, update, search
EndeavourOS  pacman      install, remove, update, search
openSUSE     zypper      install, remove, update, search

🚀 Installation
1. Quick Install
Run the following command to download and install upm:

curl -sSL https://raw.githubusercontent.com/yourusername/upm/main/upm -o /usr/local/bin/upm && \
sudo chmod +x /usr/local/bin/upm


2. Manual Install
Clone the repository:

 git clone https://github.com/yourusername/upm.git
 cd upm



Move the script to your PATH (e.g., /usr/local/bin):

 sudo cp upm /usr/local/bin/
 sudo chmod +x /usr/local/bin/upm



Verify it works:

 upm --help



💡 Usage
Basic Commands
Command
Description
upm install <pkg>
Install a package (e.g., upm install git)
upm remove <pkg>
Remove a package (e.g., upm remove git)
upm update
Update all packages
upm search <pkg>
Search for a package (e.g., upm search nginx)
upm --help
Show help message
Examples

# Install packages
upm install git nginx vim

# Remove a package
upm remove nginx

# Update the system
upm update

# Search for a package
upm search python


📝 Config File Support
You can create a config file (e.g., ~/.config/upm/packages.yaml) to list packages you want to install or manage. This is useful for restoring your setup after a fresh install.
Example Config File (packages.yaml)

packages:
  - git
  - nginx
  - vim
  - python
  - nodejs


Restore Packages from Config

upm restore ~/.config/upm/packages.yaml


Note: The restore command is a planned feature. For now, you can manually install packages from the config using a loop:

while read -r pkg; do upm install "$pkg"; done < ~/.config/upm/packages.txt


🛠️ How It Works
Distro Detection: upm reads /etc/os-release to detect your Linux distribution.

Command Mapping: It maps your command (e.g., install) to the correct package manager command for your distro.

Execution: Runs the mapped command with sudo (if required) and passes along any package names or flags.

🔧 Customization
Add Support for a New Distro
Open the upm script in a text editor.

Add your distro's ID (from /etc/os-release) to the get_pkg_manager function:

 get_pkg_manager() {
     local distro=$1
     case "$distro" in
         ubuntu|debian|pop|linuxmint) echo "apt" ;;
         fedora|rhel|centos)           echo "dnf" ;;
         arch|manjaro|endeavouros)     echo "pacman" ;;
         opensuse|suse)                echo "zypper" ;;
         yourdistro)                   echo "your_package_manager" ;;  # Add this line
         *)                            echo "unknown" ;;
     esac
 }



Add the corresponding commands for your package manager in the get_command function.

🐛 Troubleshooting
Issue
Solution
upm: command not found
Ensure upm is in your PATH (e.g., /usr/local/bin).
Permission denied
Run sudo chmod +x /usr/local/bin/upm.
Unsupported distro
Add your distro to the get_pkg_manager function.
Package not found
Check the package name for your distro (e.g., apt search <pkg>).
🤝 Contributing
Contributions are welcome! Here’s how you can help:
Report Bugs: Open an issue on GitHub.

Suggest Features: Share your ideas in the Discussions tab.

Submit Pull Requests: Fork the repo, make your changes, and submit a PR.

Local Development
Fork the repository.

Clone your fork:

 git clone https://github.com/yourusername/upm.git



Make your changes and test them:

 chmod +x upm
 ./upm install git



Commit and push your changes, then open a PR.

📜 License
This project is licensed under the MIT License – see the LICENSE file for details.
🙏 Acknowledgments
Inspired by the frustration of remembering different package manager commands.
