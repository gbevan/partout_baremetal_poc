# Baremetal Provisioning PoC

Developed in conjunction with the [Partout OpenStack PoC Project](https://github.com/gbevan/partout_openstack_poc) and
[Partout DevOps Tool](https://github.com/partoutx/partout) - Provisioning from bare metal to a private OpenStack cloud.

The project PXE boots a pair of blades from a Raspberry pi3, handing off control to Partout to provision OpenStack.

## Components

* Raspberry pi3 to use as the PXE boot server
* dnsmasq
* partout

## Force a PXEboot to reprovision a blade
WARNING: This erases the MBR boot record on your disk.
```bash
ssh controller1 -l ubuntu "sudo dd if=/dev/zero of=/dev/sda bs=512 count=1 && sudo reboot"; ssh cinder1 -l ubuntu "sudo dd if=/dev/zero of=/dev/sda bs=512 count=1 && sudo reboot"; ssh compute1 -l ubuntu "sudo dd if=/dev/zero of=/dev/sda bs=512 count=1 && sudo reboot"
```

## Reboot the Openstack hosts
```bash
ssh controller1 -l ubuntu "sudo reboot"
ssh cinder1 -l ubuntu "sudo reboot"
ssh compute1 -l ubuntu "sudo reboot"
```

## Example Wake-On-Lan script
```bash
#!/bin/bash

# Wake Manager1
wakeonlan 6c:f0:49:44:c4:93

sleep 300

# Wake Compute1
wakeonlan 6c:f0:49:44:ca:63
```

COPYRIGHT
---------
```
  Partout [Everywhere] - Policy-Based Configuration Management for the
  Data-Driven-Infrastructure.

  Copyright (C) 2015-2017 Graham Lee Bevan <graham.bevan@ntlworld.com>

  This project is part of Partout - https://github.com/partoutx/partout.

  Partout is free software: you can redistribute it and/or modify
  it under the terms of the GNU General Public License as published by
  the Free Software Foundation, either version 3 of the License, or
  (at your option) any later version.

  This program is distributed in the hope that it will be useful,
  but WITHOUT ANY WARRANTY; without even the implied warranty of
  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
  GNU General Public License for more details.

  You should have received a copy of the GNU General Public License
  along with this program.  If not, see <http://www.gnu.org/licenses/>.
```
