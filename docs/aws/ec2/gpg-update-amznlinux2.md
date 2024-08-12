# GnuPG Installation Guide

This document outlines the steps to install GnuPG and its dependencies from source on an Amazon Linux 2 system. Follow these instructions to ensure a successful installation.

## Prerequisites

Ensure that you have `sudo` privileges on your system and have `yum` package manager installed.

## Install Required Packages

First, install the necessary development tools and libraries:

```bash
sudo yum -y install bzip2 wget gcc make tar
sudo yum -y groupinstall "Development Tools"
```

## Install NPTH Library

1. Download and extract NPTH:

```bash
wget https://gnupg.org/ftp/gcrypt/npth/npth-1.6.tar.bz2
tar jxvf npth-1.6.tar.bz2
./npth-1.6/configure && make && sudo make install
```

## Install libgpg-error Library

1. Download and extract `libgpg-error`:
```bash
wget https://gnupg.org/ftp/gcrypt/gpgrt/libgpg-error-1.46.tar.bz2
tar jxvf libgpg-error-1.46.tar.bz2
./libgpg-error-1.46/configure && make && sudo make install
```

## Install libgcrypt Library

1. Download and extract `libgcrypt`:
```bash
wget https://gnupg.org/ftp/gcrypt/libgcrypt/libgcrypt-1.10.1.tar.bz2
tar jxvf libgcrypt-1.10.1.tar.bz2
./libgcrypt-1.10.1/configure && make && sudo make install
```

## Install libassuan Library

1. Download and extract `libassuan`:
```bash
wget https://gnupg.org/ftp/gcrypt/libassuan/libassuan-2.5.5.tar.bz2
tar jxvf libassuan-2.5.5.tar.bz2
./libassuan-2.5.5/configure && make && sudo make install
```

## Install libksba Library

1. Download and extract `libksba`:
```bash
wget https://gnupg.org/ftp/gcrypt/libksba/libksba-1.6.2.tar.bz2
tar jxvf libksba-1.6.2.tar.bz2
./libksba-1.6.2/configure && make && sudo make install
```

## Install GnuPG

1. Download and verify GnuPG:
```bash
wget https://www.gnupg.org/ftp/gcrypt/gnupg/gnupg-2.3.8.tar.bz2
wget https://www.gnupg.org/ftp/gcrypt/gnupg/gnupg-2.3.8.tar.bz2.sig
gpg --verify gnupg-2.3.8.tar.bz2.sig gnupg-2.3.8.tar.bz2
tar jxvf gnupg-2.3.8.tar.bz2
./gnupg-2.3.8/configure && make && sudo make install
```

## Verify Installation

1. Verify that the `gpg` binary is correctly placed:

    ```bash
    sudo mv /usr/local/bin/gpg /usr/bin/gpg
    ```

2. Check the GnuPG version to ensure the installation was successful:

    ```bash
    gpg --version
    ```
## Troubleshooting

**If you encounter an error such as `error while loading shared libraries: libgcrypt.so.20: cannot open shared object file: No such file or directory`, ensure that `/usr/local/lib` is correctly added to the system's library cache and try running `gpg --version` again.**

## Update System’s Library Cache

1. Create a configuration file for the library path:

    ```bash
    echo "/usr/local/lib" | sudo tee /etc/ld.so.conf.d/local-lib.conf
    ```

2. Update the library cache:

    ```bash
    sudo ldconfig
    ```