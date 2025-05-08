# How to restore the default yum repositories on Rocky Linux 9

---

## Method 1: Reinstall rocky-repos using dnf ( if you still have a working repo )

if your system is still connected to the internet and at least one repo is funcitonal, run:

```bash
sudo dnf install rocky-repos
```

This will restore all the official .repo files in /etc/yum.repos.d/.

## Method 2: Manually download and install rocky-repos RPM

if dnf doesn't work due to missing repos:

1. Download the package:

```bash
sudo curl -O https://download.rockylinux.org/pub/rocky/9/BaseOS/x86_64/os/Packages/r/rocky-repos-9.5-1.3.el9.noarch.rpm
```

2. Install it:

```bash
sudo rpm -ivh rocky-repos-9.5-1.3.el9.noarch.rpm
```

## Method 3: Install RPM locally using dnf

if you already have the RPM file (e.g.,copied from another machine):

```bash
sudo dnf install rocky-repos-9.5-1.3.el9.noarch.rpm
```
This method handles dependencies better than rpm.


## TroubleShooting

- Problem:

```bash
[admin@jenkins yum.repos.d]$ sudo rpm -ivh rocky-repos-9.5-1.3.el9.noarch.rpm
warning: rocky-repos-9.5-1.3.el9.noarch.rpm: Header V4 RSA/SHA256 Signature, key ID 350d275d: NOKEY
error: Failed dependencies:
	system-release = 9.5-1.3.el9 is needed by rocky-repos-9.5-1.3.el9.noarch
```

- Solution:

Download rocky-release-9.5-1.3.el9.noarch.rpm package and install it.

```bash
sudo curl -O https://download.rockylinux.org/pub/rocky/9/BaseOS/x86_64/os/Packages/r/rocky-release-9.5-1.3.el9.noarch.rpm
```

```bash
sudo rpm -Uvh rocky-release-9.5-1.3.el9.noarch.rpm
```

Then Install rocky-repos-9.5-1.3.el9.noarch.rpm again

```bash
sudo rpm -ivh rocky-repos-9.5-1.3.el9.noarch.rpm
```

- Problem: 

```bash
I have already install rocky-repos-9.5-1.3.el9.noarch.rpm again, but I delete /etc/yum.repos.d/*.repo
```

- Solution:

```bash
sudo rpm -Uvh --replacepkgs rocky-repos-9.5-1.3.el9.noarch.rpm
```
