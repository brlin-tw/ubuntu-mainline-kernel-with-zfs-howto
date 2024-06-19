# How to build the ZFS kernel module against a Ubuntu mainline kernel

Documents the process of building a recent version ZFS kernel module against a Ubuntu mainline kernel version, and the details on how to make it work properly in runtime.

<https://gitlab.com/brlin/ubuntu-mainline-kernel-with-zfs-howto>  
[![The GitLab CI pipeline status badge of the project's `main` branch](https://gitlab.com/brlin/ubuntu-mainline-kernel-with-zfs-howto/badges/main/pipeline.svg?ignore_skipped=true "Click here to check out the comprehensive status of the GitLab CI pipelines")](https://gitlab.com/brlin/ubuntu-mainline-kernel-with-zfs-howto/-/pipelines) [![GitHub Actions workflow status badge](https://github.com/brlin-tw/ubuntu-mainline-kernel-with-zfs-howto/actions/workflows/check-potential-problems.yml/badge.svg "GitHub Actions workflow status")](https://github.com/brlin-tw/ubuntu-mainline-kernel-with-zfs-howto/actions/workflows/check-potential-problems.yml) [![pre-commit enabled badge](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white "This project uses pre-commit to check potential problems")](https://pre-commit.com/) [![REUSE Specification compliance badge](https://api.reuse.software/badge/gitlab.com/brlin/ubuntu-mainline-kernel-with-zfs-howto "This project complies to the REUSE specification to decrease software licensing costs")](https://api.reuse.software/info/gitlab.com/brlin/ubuntu-mainline-kernel-with-zfs-howto)

## The problem

The AMDGPU driver shipped in the Ubuntu 24.04 kernel contains a issue that may cause system instability after some videos are played on a Framework Laptop 13(AMD 7040 series) system.  I would like to install a recent [mainline kernel](https://kernel.ubuntu.com/mainline/) built by Ubuntu to check whether the issue can still be reproduced, however it failed to boot due to the missing ZFS driver which is used as the storage system in my system.  Installing the `zfs-dkms` package doesn't work either as it isn't compatible with newer kernel versions.

## The solution

I would like to build the recent version ZFS kernel against the mainline kernel version to allow the system to boot without rebuilding the entire Linux kernel.

## Install a mainline kernel

Download the desired kernel package from the [Ubuntu Mainline Kernel PPA Archive Ubuntu https://kernel.ubuntu.com › ~kernel-ppa](https://kernel.ubuntu.com/~kernel-ppa/mainline/) and install it using the following terminal command as root:

```bash
sudo apt install /path/to/linux-*.deb
```

**WARNING:** Be careful not to accidentally install unrelated kernel packages.  You may check how the `/path/to/linux-*.deb` glob pattern expanded by running the following command in the terminal:

```bash
echo /path/to/linux-*.deb
```

You can also use [the Mainline Kernels utility](https://github.com/bkw777/mainline) to install and manage Ubuntu mainline kernels.

This kernel will currently not be able to boot the system as it does not have the required driver to mount the root filesystem on the ZFS storage system.

## Licensing

Unless otherwise noted(individual file's header/[REUSE DEP5](.reuse/dep5)), this product is licensed under [the 4.0 International version of the Creative Commons Attribution-ShareAlike license](https://creativecommons.org/licenses/by-sa/4.0/), or any of its more recent versions of your preference.

This work complies to [the REUSE Specification](https://reuse.software/spec/), refer the [REUSE - Make licensing easy for everyone](https://reuse.software/) website for info regarding the licensing of this product.
