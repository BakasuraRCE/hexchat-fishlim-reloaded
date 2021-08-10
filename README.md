HexChat FiSHLiM Reloaded
========================

Adds FiSHLiM support to HexChat with with steroids!

Based on FiSHLiM plugin of HexChat.

Installation
------------

### Dependencies

- gio
- openssl
- hexchat
- meson

### Conflicts

You must deactivate the original FiSHLiM version of the HexChat core before using this version

#### User install

```sh
meson builddir -Dlocal_install=true
ninja -C builddir test
ninja -C builddir install
```

#### System install

```sh
meson builddir
ninja -C builddir
ninja -C builddir test
sudo ninja -C builddir install
```

### AUR

We offer AUR repo: https://aur.archlinux.org/packages/hexchat-fishlim-reloaded-git/

Features
--------

- Backward compatibility with the database file addon_fishlim.conf from original HexChat module
- CBC mode on SETKEY and KEYX commands
- Store keys in CBC mode (addon_fishlim.conf)
- Detect context in DELKEY command
- Encrypted flag for incoming and outgoing messages

Usage
-----

- SETKEY command
  - for CBC mode -> /setkey cbc:key
  - for ECB mode -> /setkey ecb:key
  - for ECB mode -> /setkey key

Part of HexChat
---------------

This project is intended to provide users with the new features until they are merged into the HexChat core: https://github.com/hexchat/hexchat/pull/2347
