Subject: Fix for "Internal error on command: 'PRTOUCH_PROBE_ZOFFSET'"

The original repository has an issue with the PRTouch Z-offset probe, leading to an "Internal error on command: 'PRTOUCH_PROBE_ZOFFSET'".
The problem consists of two parts:
    Outdated methods: The register_response method in prtouch.py and hx711s.py was deprecated. (Note: This was partially addressed in a recent update with register_serial_response).
    Immutable tuple error: In prtouch.py, the code attempts to modify z_probe, which is a tuple. Since tuples in Python are immutable, this triggers a TypeError.

Solution:
I've implemented a fix by converting the z_probe tuple into a list before modification and then converting it back to a tuple to maintain compatibility with the rest of the code.

Changes in line 432:

  Old code:
    z_probe[2] = homing_origin[2] + z_adjust - start_z_offset

  New code:
    z_list = list(z_probe)
    z_list[2] = homing_origin[2] + z_adjust - start_z_offset
    z_probe = tuple(z_list)

This fix restores the intended functionality of the PRTouch probe. I have had this problem for a while, and this solution resolved the issue for my setup. So i decided to post it for anyone else running into this problem.
I also keep my set of updated configuration files for the Ender 3 V3 SE with automatic KAMP and PRTouch probe which you can find here: https://github.com/Seerafimm/Ender-3v3-SE-Klipper-configuration-files










Welcome to the Klipper project!

[![Klipper](docs/img/klipper-logo-small.png)](https://www.klipper3d.org/)

https://www.klipper3d.org/

The Klipper firmware controls 3d-Printers. It combines the power of a
general purpose computer with one or more micro-controllers. See the
[features document](https://www.klipper3d.org/Features.html) for more
information on why you should use the Klipper software.

Start by [installing Klipper software](https://www.klipper3d.org/Installation.html).

Klipper software is Free Software. See the [license](COPYING) or read
the [documentation](https://www.klipper3d.org/Overview.html). We
depend on the generous support from our
[sponsors](https://www.klipper3d.org/Sponsors.html).
