# Welcome to arch-pkgs

## Package list: base + Intel + Android (non-graphical)

This repository provides `base-ia.txt`: a plain-text package list intended for use with `pacstrap` during an Arch Linux install.

### Important: enable multilib (required for lib32 packages)

`base-ia.txt` includes `lib32-vulkan-intel`, which requires the `multilib` repository.

Edit `/etc/pacman.conf`:

```sh
vim /etc/pacman.conf
```

Find the `[multilib]` section and **uncomment** it (and its `Include = ...` line), then refresh package databases:

```sh
sudo pacman -Syy
```

**What it includes (high level):**
- Base system + build tools (base, base-devel, kernel + headers, firmware)
- Core CLI utilities (git, wget, zip/unzip, man-db, sudo, etc.)
- Terminal/QoL tools (fzf, bat, lsd, zoxide, glow)
- Fonts (DejaVu, Terminus, Awesome Terminal Fonts)
- Networking + services (NetworkManager, OpenSSH, Avahi)
- Intel support (microcode + Intel graphics/Vulkan + tooling)
- Android tooling (adb/fastboot + udev rules)
- Bootloader utilities (EFI + GRUB)

### File

- `base-ia.txt` — one package name per line

### Using the list with pacstrap

```sh
pacstrap -K /mnt $(< base-ia.txt)
```

Replace `/mnt` with your target mount point.

## Package list: PipeWire + ALSA + BlueZ (Sound & Bluetooth)

This repository provides `sound.txt`: a plain-text package list intended for use with `pacman` after Arch Linux is installed.

**What it includes (high level):**
- PipeWire audio server + compatibility layers (ALSA, PulseAudio, JACK)
- WirePlumber session manager
- ALSA utilities/tools (mixer, troubleshooting)
- Bluetooth stack (BlueZ) for wireless headsets
- A TUI mixer (`pulsemixer`) for quick volume/device control

### File

- `sound.txt` — one package name per line

### Installing the packages

```sh
sudo pacman -S --needed $(< sound.txt)
```

### Enable Bluetooth (for headsets)

```sh
sudo systemctl enable --now bluetooth
```

### Ensure PipeWire is running (per-user)

On most setups this starts automatically. If it doesn’t:

```sh
systemctl --user enable --now wireplumber
systemctl --user enable --now pipewire pipewire-pulse
```

### Pair/connect a headset (bluetoothctl)

```sh
bluetoothctl
```

Common commands inside `bluetoothctl`:

```text
power on
agent on
default-agent
scan on
pair <MAC>
trust <MAC>
connect <MAC>
```

