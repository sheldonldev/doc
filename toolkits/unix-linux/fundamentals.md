# Fundamentals

What is Unix/Linux

* Unix/Linux is the operating system `kernel`, which started by the boot loader, which itself started by the BIOS/UEFI;
* Ensures coordination between hardware and software, including managing hardware, processing, users, permissions, and the file system;
* Provides common base to all programs, runs in `ring zero` \(`kernel space`\);
* Everything out kernel is `user space`;





* `Power On` - `BIOS` - `MBR (First Sector of the Hard Disk)` - `Boot Loader` - `Kernel` - `initramfs` - `/sbin/init` - `Shell by getty` - `(X Windows System) GUI`
* `/sbin/init`:
  * Traditionally, `/sbin/init` is serial processes `SysVinit`, did not easily take advantage of the _parallel processing_. Some modern methods, such as the use of containers, can require almost instantaneous startup times. Thus, systems now require methods with faster and enhanced capabilities
  * `Upstart` Developed by Ubuntu and first included in 2006; Adopted in Fedora 9 \(in 2008\) and in RHEL 6 and its clones.
  * `systemd` Adopted by Fedora first \(in 2011\); Adopted by RHEL 7 and SUSE; Replaced Upstart in Ubuntu 16.04; Replaced `Upstart` in Ubuntu 16.04. It has been adopted by the major distributions
  * `/sbin/init` now just points to `/lib/systemd/systemd`;

```text
# start|stop|restart|enable|disablesudo systemctl start|stop|restart nfs.servicesudo systemctl enable|disable nfs.service# Confirmsudo ss -antlp | grep [service]# List all available servicessystemctl list-unit-fileslsof -i -P -n
```

