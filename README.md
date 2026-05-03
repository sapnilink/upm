# 🚀 upm

**Unified Package Manager for Linux**

**upm** is a lightweight, cross-distro wrapper for Linux package managers. It provides a unified syntax for installing, removing, updating, and searching packages across different Linux distributions—so you never have to remember whether it's `apt`, `dnf`, `pacman`, or `zypper` again.

Whether you're switching distros, managing multiple systems, or just tired of Googling package manager commands, **upm** has you covered.

---

## ✨ Features

* ✅ **Unified Syntax** – Use the same commands (`install`, `remove`, `update`, `search`) across all supported distros
* ✅ **Distro Detection** – Automatically detects your Linux distribution and uses the correct package manager
* ✅ **Simple & Fast** – No dependencies, just a single bash script
* ✅ **Config Support** – Restore your packages from a config file after a fresh install
* ✅ **Extensible** – Easy to add support for new distros or package managers

---

## 📋 Supported Distros & Package Managers

| Distro      | Package Manager | Supported Actions               |
| ----------- | --------------- | ------------------------------- |
| Ubuntu      | apt             | install, remove, update, search |
| Debian      | apt             | install, remove, update, search |
| Fedora      | dnf             | install, remove, update, search |
| RHEL/CentOS | dnf             | install, remove, update, search |
| Arch Linux  | pacman          | install, remove, update, search |
| Manjaro     | pacman          | install, remove, update, search |
| EndeavourOS | pacman          | install, remove, update, search |
| openSUSE    | zypper          | install, remove, update, search |

---

## 🚀 Installation

### Quick Install

```bash
curl -sSL https://raw.githubusercontent.com/yourusername/upm/main/upm -o /usr/local/bin/upm && \
sudo chmod +x /usr/local/bin/upm
```

### Manual Install

```bash
git clone https://github.com/yourusername/upm.git
cd upm
```

Move the script to your PATH:

```bash
sudo cp upm /usr/local/bin/
sudo chmod +x /usr/local/bin/upm
```

Verify installation:

```bash
upm --help
```

---

## 💡 Usage

### Basic Commands

| Command             | Description          |
| ------------------- | -------------------- |
| `upm install <pkg>` | Install a package    |
| `upm remove <pkg>`  | Remove a package     |
| `upm update`        | Update all packages  |
| `upm search <pkg>`  | Search for a package |
| `upm --help`        | Show help message    |

### Examples

```bash
# Install packages
upm install git nginx vim

# Remove a package
upm remove nginx

# Update the system
upm update

# Search for a package
upm search python
```

---

## 📝 Config File Support

You can create a config file (e.g., `~/.config/upm/packages.yaml`) to list packages you want to install or manage. This is useful for restoring your setup after a fresh install.

### Example (`packages.yaml`)

```yaml
packages:
  - git
  - nginx
  - vim
  - python
  - nodejs
```

### Restore Packages (Planned Feature)

```bash
upm restore ~/.config/upm/packages.yaml
```

> ⚠️ Note: This feature is planned but not yet implemented.

### Temporary Workaround

```bash
while read -r pkg; do upm install "$pkg"; done < ~/.config/upm/packages.txt
```

---

## 🛠️ How It Works

* **Distro Detection:** Reads `/etc/os-release` to identify your Linux distribution
* **Command Mapping:** Maps your command (e.g., `install`) to the correct package manager
* **Execution:** Runs the mapped command with `sudo` (if required)

---

## 🔧 Customization

### Add Support for a New Distro

Edit the `upm` script and update:

```bash
get_pkg_manager() {
    local distro=$1
    case "$distro" in
        ubuntu|debian|pop|linuxmint) echo "apt" ;;
        fedora|rhel|centos)           echo "dnf" ;;
        arch|manjaro|endeavouros)     echo "pacman" ;;
        opensuse|suse)                echo "zypper" ;;
        yourdistro)                   echo "your_package_manager" ;;
        *)                            echo "unknown" ;;
    esac
}
```

Then add corresponding commands in `get_command`.

---

## 🐛 Troubleshooting

| Issue                    | Solution                                    |
| ------------------------ | ------------------------------------------- |
| `upm: command not found` | Ensure it's in your PATH (`/usr/local/bin`) |
| Permission denied        | Run `sudo chmod +x /usr/local/bin/upm`      |
| Unsupported distro       | Add your distro in `get_pkg_manager`        |
| Package not found        | Verify package name for your distro         |

---

## 🤝 Contributing

Contributions are welcome!

* 🐞 Report bugs via GitHub Issues
* 💡 Suggest features in Discussions
* 🔧 Submit pull requests

### Local Development

```bash
git clone https://github.com/yourusername/upm.git
cd upm
chmod +x upm
./upm install git
```

---

## 📜 License

This project is licensed under the **MIT License**. See the `LICENSE` file for details.

---

## 🙏 Acknowledgments

Inspired by the frustration of remembering different package manager commands.
