---
title:  "[draft]The Linux boot process"
date:   2016-12-10 23:20:07 +0200
categories: jekyll update
---

#### [System initialization:](https://wiki.archlinux.org/index.php/Arch_boot_process#System_initialization)
>##### Under BIOS:
1. System switched on - [Power-on self-test](https://en.wikipedia.org/wiki/Power-on_self-test) or POST process
2. After POST, BIOS initializes the necessary system hardware for booting (disk, keyboard controllers etc.)
3. BIOS launches the first 440 bytes ([Master Boot Record](https://wiki.archlinux.org/index.php/Partitioning#Master_Boot_Record)) of the first disk in the BIOS disk order
4. The MBR boot code then takes control from BIOS and launches its next stage code (if any) (mostly boot loader code)
5. The launched actual boot loader

>##### Under UEFI:
1. System switched on. The Power On Self Test (POST) is executed.
2. UEFI firmware is loaded. Firmware initializes the hardware required for booting.
3. Firmware reads the boot entries in the firmware's boot manager to determine which UEFI application to be launched and from where (i.e. from which disk and partition).
4. Firmware launches the UEFI application.
  - This could be the Arch kernel itself (since EFISTUB is enabled by default).
  - It could be some other application such as a shell or a graphical boot manager.
  - Or the boot entry could simply be a disk. In this case the firmware looks for an EFI System Partition on that disk and tries to run the fallback UEFI application \EFI\BOOT\BOOTX64.EFI (BOOTIA32.EFI on 32-bit systems). This is how UEFI bootable thumb drives work.


Thanks to the excellent ArchLinux documentation we know that in most of the case when you switch the system on the firmware on your motherboard takes care about your hardware and will launch the boot loader that in the majority of the case is [GRUB2](https://wiki.archlinux.org/index.php/GRUB).


initrd, init first process.
