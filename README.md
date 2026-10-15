# 🌤️ gweather-add-loc

A simple, standalone Bash script to add custom locations with arbitrary coordinates to **GNOME Weather** (`org.gnome.Weather`) via `gsettings`.

Works with both **native packages** and **Flatpak** installations on **GNOME 40+ / libgweather-4**.

## ✨ Features

* Automatically detects **Flatpak** vs. **native package** installations
* Converts decimal degrees to radians with proper leading-zero formatting
* Formats and injects the exact `libgweather-4` GVariant data structure
* Gracefully restarts GNOME Weather to apply changes immediately

## 📌 Prerequisites

The script requires `bc` for floating-point calculations:

* **Fedora:** `sudo dnf install bc`
* **Debian/Ubuntu:** `sudo apt install bc`
* **Arch Linux:** `sudo pacman -S bc`
* **Homebrew:** `brew install bc`

## 🚀 Installation

Clone the repository and make the script executable:

```bash
git clone https://github.com/e1dred/gweather-add-loc.git
cd gweather-add-loc
chmod +x gweather-add-loc.sh
```

## ⚙️ Usage 

```bash
./gweather-add-loc.sh "Location Name" LATITUDE LONGITUDE
```
You can search for the latitude and longitude of a location here: https://www.latlong.net/

### 💡 Example

Add Bishkek, Kyrgyzstan:
```bash
./gweather-add-loc.sh "Bishkek, Kyrgyzstan" 42.882004 74.582748
```

The script automatically converts the coordinates to radians, formats the `libgweather-4` GVariant string, updates `gsettings`, and restarts `gnome-weather` to apply the changes.
