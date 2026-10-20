---
title: Part 4 - Lessons learned
---

# Part 4: Lessons learned

Problems hit while building the lab, and what fixed them.

## The VM disk filled up during the Wazuh install

The Wazuh installer failed at the dashboard step and rolled everything back.

![No space left on device during dpkg](images/lesson-disk-full-error.png)

The log showed `No space left on device`. The VM disk was 25 GB. I resized the
virtual disk to 60 GB, then grew the partition and filesystem:

```bash
sudo apt install -y cloud-guest-utils
sudo growpart /dev/sda 3
sudo resize2fs /dev/sda3
```

The re-run installed cleanly. **Lesson:** a SIEM needs real disk space; size the
VM for the install and the logs it will collect.

## VMs were slow because everything sat on a spinning disk

Three VMs installing at once on a hard disk pushed it past 100% busy, with
30-60 ms per I/O. Moving the VM files to an SSD fixed it. **Lesson:** check where
the VM files live before blaming the CPU.

## Copy-paste did not work in the Ubuntu VM

Two causes, found by checking the session and the running processes:

- Ubuntu 22.04 used a Wayland session, and the VirtualBox clipboard service
  only works on Xorg. Fix: set `WaylandEnable=false` in `/etc/gdm3/custom.conf`.
- Guest Additions 6.1.50 (from apt) and 7.2.6 (from the CD) were both installed
  and conflicted. Fix: keep only the matching version and start
  `VBoxClient --clipboard` from an autostart entry.

**Lesson:** match guest tools to the hypervisor version, and verify with
`pgrep -a VBoxClient` instead of assuming.

## A user without sudo

The unattended installer created a user that was not in the `sudo` group. I fixed
it from a live ISO by mounting the root partition and adding the user to the
group. **Lesson:** verify privileges early.

## Segmenting the network

Each VM got a NAT adapter (internet) and a second adapter on an isolated NAT
Network. The lab traffic stays off the home network, which matters once the lab
runs anything you do not want near other devices.
