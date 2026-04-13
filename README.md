# arch-pkgs

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



