# FreeBSD Unofficial Port: gcc14-ada

> **Note**
> This port is unofficial and maintained separately from the FreeBSD Ports Collection.
> It is based on modifications to `/usr/ports/lang/gcc14` to enable Ada support.

By default, the official `lang/gcc14` port does not include Ada (GNAT). This port modifies the build to enable Ada and package the GNAT toolchain alongside GCC.

## Features

- GCC 14 with Ada frontend (GNAT)
- Includes all GNAT utilities (`gnatmake`, `gnatbind`, `gnatchop`, etc.)
- Installs Ada runtime libraries (`libgnat`, `adalib`, `adainclude`)
- Packaged as `gcc14-ada` for easy installation and distribution

## Requirements

- FreeBSD 14.3 or later
- A bootstrap Ada compiler `gnat13`

## Installation

Clone this repository into your FreeBSD ports tree:

```sh
cd /usr/ports/lang
git clone https://github.com/hodong-kim/gcc14-ada.git
cd gcc14-ada
```

Build and install:

```sh
# Install bootstrap compiler
sudo pkg install gnat13

# Add gnat13 to PATH for this session
export PATH=/usr/local/gnat13/bin:$PATH
make package
sudo make reinstall
```

Alternatively, install the generated package manually:

```sh
sudo pkg add ./work/pkg/gcc14-ada-14.x.x.pkg
```

Remove gnat13 if previously installed:

```
sudo pkg remove gnat13
```

## Verification

After installation, confirm Ada support:

```sh
pkg info gcc14-ada
gnat14 --version
gcc14 -v
```

You should see `GNAT 14.x.x` and `--enable-languages=...,ada` in the GCC configuration output.
