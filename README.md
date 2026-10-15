# 🌤️ gweather-add-loc

![License](https://img.shields.io/github/license/e1dred/gweather-add-loc)
![Shell](https://img.shields.io/badge/shell-bash-4EAA25)
![GNOME](https://img.shields.io/badge/GNOME-40%2B-4A86CF)

> Add custom locations with arbitrary coordinates to GNOME Weather from the command line.

A simple, standalone Bash script that adds locations to **GNOME Weather** (`org.gnome.Weather`) via `gsettings`. It works with both **native packages** and **Flatpak** installations on **GNOME 40+ / libgweather-4**.

<!-- Add a screenshot of GNOME Weather showing an added location, then uncomment:
![GNOME Weather showing a custom location](docs/screenshot.png)
-->

## ✨ Features

- Automatically detects **Flatpak** vs. **native package** installations
- Converts decimal degrees to **radians** with proper leading-zero formatting
- Formats and injects the exact **`libgweather-4` GVariant** data structure
- Gracefully **restarts GNOME Weather** to apply changes immediately

## Prerequisites

The script requires `bc` for floating-point calculations:

```bash
# Fedora
sudo dnf install bc

# Debian / Ubuntu
sudo apt install bc

# Arch Linux
sudo pacman -S bc

# Universal Blue distros Bluefin, Aurora, Bazzite (Homebrew)
brew install bc
```

> [!NOTE]
> Universal Blue distros such as Bluefin, Aurora, and Bazzite are image-based and use Homebrew for command-line tools, so use the `brew` command above rather than `dnf`.

## Installation

Clone the repository from either GitLab or GitHub, then make the script executable.

> [!NOTE]
> This project is developed on [GitLab](https://gitlab.com/e1dred-group/gweather-add-loc) and automatically mirrored to [GitHub](https://github.com/e1dred/gweather-add-loc). Both copies are identical, so use whichever you prefer.

### Option A: GitLab

```bash
git clone https://gitlab.com/e1dred-group/gweather-add-loc.git
cd gweather-add-loc
chmod +x gweather-add-loc.sh
```

### Option B: GitHub

```bash
git clone https://github.com/e1dred/gweather-add-loc.git
cd gweather-add-loc
chmod +x gweather-add-loc.sh
```

## Usage

```bash
./gweather-add-loc.sh "Location Name" LATITUDE LONGITUDE
```

| Argument | Description | Example |
|---|---|---|
| `Location Name` | Display name. Quote it if it contains spaces. | `"Bishkek, Kyrgyzstan"` |
| `LATITUDE` | Decimal degrees. Use a negative value for south. | `42.882004` |
| `LONGITUDE` | Decimal degrees. Use a negative value for west. | `74.582748` |

Need coordinates? Look them up with [Find My Coordinates](https://findmycoordinates.com/find-coordinates).

### 💡 Examples

Add Bishkek, Kyrgyzstan:

```bash
./gweather-add-loc.sh "Bishkek, Kyrgyzstan" 42.882004 74.582748
```

Add Buenos Aires, Argentina (negative latitude and longitude):

```bash
./gweather-add-loc.sh "Buenos Aires, Argentina" -34.6037 -58.3816
```

> [!NOTE]
> GNOME Weather is restarted automatically so the new location appears right away.

## How it works

The script converts the coordinates you provide from decimal degrees to radians, then builds the `libgweather-4` GVariant string that GNOME Weather expects. It writes that string to the app's `gsettings` entry, using the Flatpak or native configuration depending on which installation it finds, and finally restarts `gnome-weather` to apply the change.

## Troubleshooting

| Problem | What to try |
|---|---|
| `bc: command not found` | Install `bc` (see [Prerequisites](#prerequisites)). |
| `Permission denied` | Make the script executable: `chmod +x gweather-add-loc.sh`. |
| Location doesn't appear | Fully quit GNOME Weather and reopen it. |
| Wrong position on the map | Check the argument order (latitude first) and the sign of each value. |

To remove a location you added, delete it from within GNOME Weather itself.

## Compatibility

- GNOME 40 or newer (`libgweather-4`)
- Native and Flatpak installations of GNOME Weather

<!-- Optionally list the distros and GNOME versions you've tested on. -->

## License

See the [LICENSE](LICENSE) file for details.