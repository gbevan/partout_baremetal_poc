# Baremetal Provisioning PoC

Developed in conjunction with the [Partout OpenStack PoC Project](https://github.com/gbevan/partout_openstack_poc) and
[Partout DevOps Tool](https://github.com/partoutx/partout) - Provisioning from bare metal to a private OpenStack cloud.

The project PXE boots a pair of blades from a Raspberry pi3, handing off controller to Partout to provision OpenStack.

## Components

* Raspberry pi3 to use as the PXE boot server
* dnsmasq
* partout

## Force a PXEboot to reprovision a blade
WARNING: This erases the MBR boot record on your disk.
```bash
ssh manager1 -l ubuntu "sudo dd if=/dev/zero of=/dev/sda bs=512 count=1 && sudo reboot"
ssh compute1 -l ubuntu "sudo dd if=/dev/zero of=/dev/sda bs=512 count=1 && sudo reboot"
```
