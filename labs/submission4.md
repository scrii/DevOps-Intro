# **Lab 4 — Operating Systems & Networking**

## **Task 1 — Operating System Analysis**

### Task 1.1 — Boot Performance Analysis

1. System Boot Time Analysis

```bash
maks@maks-VirtualBox:~$ systemd-analyze
Startup finished in 5.910s (kernel) + 30.210s (userspace) = 36.121s 
graphical.target reached after 30.156s in userspace.

maks@maks-VirtualBox:~$ systemd-analyze blame
22.512s plymouth-quit-wait.service
 8.084s fwupd-refresh.service
 2.408s apport.service
 2.379s NetworkManager.service
 2.239s snapd.seeded.service
 2.186s fwupd.service
 2.097s snapd.service
 2.034s dev-sda2.device
 1.759s dev-loop8.device
 1.404s gnome-remote-desktop.service
 1.216s systemd-tmpfiles-clean.service
 1.168s power-profiles-daemon.service
 1.145s polkit.service
 1.102s rsyslog.service
 1.095s accounts-daemon.service
 1.049s gpu-manager.service
 1.038s udisks2.service
  945ms dev-loop10.device
  939ms dev-loop1.device
  904ms dev-loop0.device
  898ms avahi-daemon.service
  894ms dev-loop7.device
  890ms apparmor.service
  830ms dbus.service
  830ms snapd.apparmor.service
  827ms dev-loop6.device
  825ms dev-loop5.device
  825ms dev-loop4.device
  824ms dev-loop2.device
  822ms dev-loop3.device
  707ms grub-common.service
  639ms systemd-udevd.service
  596ms ModemManager.service
  535ms systemd-resolved.service
  535ms user@1000.service
  521ms dev-loop9.device
  517ms upower.service
  499ms systemd-binfmt.service
  497ms systemd-modules-load.service
  496ms switcheroo-control.service
  495ms e2scrub_reap.service
  439ms systemd-udev-trigger.service
  375ms systemd-journal-flush.service
  363ms NetworkManager-wait-online.service
  336ms grub-initrd-fallback.service
  297ms systemd-timesyncd.service
  293ms gdm.service
  291ms systemd-tmpfiles-setup.service
  287ms systemd-logind.service
  281ms dev-loop11.device
  279ms systemd-oomd.service
  276ms systemd-hostnamed.service
  225ms update-notifier-download.service
  220ms keyboard-setup.service
  217ms systemd-journald.service
  217ms systemd-tmpfiles-setup-dev-early.service
  211ms snap-firefox-7766.mount
  211ms cups.service
  188ms plymouth-start.service
  186ms systemd-sysctl.service
  182ms wpa_supplicant.service
  181ms snap-firmware\x2dupdater-210.mount
  159ms sysstat.service
  156ms kerneloops.service
  155ms colord.service
  153ms snap-gnome\x2d42\x2d2204-247.mount
  141ms snap-snap\x2dstore-1270.mount
  134ms snap-snapd-25935.mount
  132ms snap-bare-5.mount
  130ms snap-snapd\x2ddesktop\x2dintegration-343.mount
  128ms snap-gtk\x2dcommon\x2dthemes-1535.mount
  118ms snap-core22-2292.mount
  115ms dev-hugepages.mount
  113ms dev-loop12.device
  112ms dev-mqueue.mount
  107ms sys-kernel-debug.mount
  106ms rtkit-daemon.service
  105ms snap-telegram\x2ddesktop-6899.mount
  103ms sys-kernel-tracing.mount
   98ms systemd-remount-fs.service
   92ms systemd-random-seed.service
   91ms swap.img.swap
   86ms proc-sys-fs-binfmt_misc.mount
   83ms sys-fs-fuse-connections.mount
   69ms kmod-static-nodes.service
   68ms modprobe@dm_mod.service
   66ms modprobe@configfs.service
   63ms modprobe@efi_pstore.service
   58ms plymouth-read-write.service
   58ms modprobe@drm.service
   55ms snap-mesa\x2d2404-1165.mount
   53ms console-setup.service
   50ms sys-kernel-config.mount
   42ms systemd-update-utmp.service
   40ms snapd.socket
   39ms systemd-user-sessions.service
   38ms snap-gnome\x2d46\x2d2404-153.mount
   35ms openvpn.service
   34ms modprobe@fuse.service
   32ms user-runtime-dir@1000.service
   32ms systemd-tmpfiles-setup-dev.service
   31ms alsa-restore.service
   30ms ufw.service
   29ms modprobe@loop.service
   28ms snap-core24-1349.mount
   28ms sysstat-collect.service
   27ms systemd-update-utmp-runlevel.service
   20ms setvtrgb.service
```

2. System Load Check

```bash
maks@maks-VirtualBox:~$ uptime
 22:41:51 up 30 min,  1 user,  load average: 1.19, 1.07, 1.00
 
maks@maks-VirtualBox:~$ w
 22:41:59 up 30 min,  1 user,  load average: 1.08, 1.05, 1.00
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU  WHAT
maks     tty2     -                22:11   13:44   0.39s  0.34s /usr/libexec/gn
```

### Task 1.2 — Process Forensics

1. Identify Resource-Intensive Processes

```bash
maks@maks-VirtualBox:~$ ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head -n 6
    PID    PPID CMD                         %MEM %CPU
   4132    1411 /snap/snap-store/1270/bin/s 13.1 15.9
   6553    1184 /snap/telegram-desktop/6899 11.2 11.7
   1411    1184 /usr/bin/gnome-shell        10.2 18.1
   2578    1411 /snap/firefox/7766/usr/lib/ 10.1 21.4
   7343    1411 /usr/bin/gnome-text-editor   8.4 19.2

maks@maks-VirtualBox:~$ ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head -n 6
    PID    PPID CMD                         %MEM %CPU
   7571    7312 ps -eo pid,ppid,cmd,%mem,%c  0.1  100
   2578    1411 /snap/firefox/7766/usr/lib/ 10.1 21.1
   7343    1411 /usr/bin/gnome-text-editor   8.4 18.5
   1411    1184 /usr/bin/gnome-shell        10.2 18.3
   4132    1411 /snap/snap-store/1270/bin/s 13.1 15.6

wtmp begins Fri Feb 27 21:57:05 2026
```

### **Task 1.3 — Service Dependencies**

1. Map Service Relationships

```bash
maks@maks-VirtualBox:~$ systemctl list-dependencies
default.target
● ├─accounts-daemon.service
● ├─gdm.service
● ├─gnome-remote-desktop.service
● ├─power-profiles-daemon.service
● ├─switcheroo-control.service
○ ├─systemd-update-utmp-runlevel.service
● ├─udisks2.service
● └─multi-user.target
○   ├─anacron.service
●   ├─apport.service
●   ├─avahi-daemon.service
●   ├─console-setup.service
●   ├─cron.service
●   ├─cups-browsed.service
●   ├─cups.path
●   ├─cups.service
●   ├─dbus.service
○   ├─dmesg.service
○   ├─e2scrub_reap.service
○   ├─grub-common.service
○   ├─grub-initrd-fallback.service
●   ├─kerneloops.service
●   ├─ModemManager.service
○   ├─networkd-dispatcher.service
●   ├─NetworkManager.service
○   ├─open-vm-tools.service
●   ├─openvpn.service
●   ├─plymouth-quit-wait.service
○   ├─plymouth-quit.service
●   ├─rsyslog.service
○   ├─run-vmblock\x2dfuse.mount
○   ├─secureboot-db.service
●   ├─snap-bare-5.mount
●   ├─snap-core22-2292.mount
●   ├─snap-core24-1349.mount
●   ├─snap-firefox-7766.mount
●   ├─snap-firmware\x2dupdater-210.mount
●   ├─snap-gnome\x2d42\x2d2204-247.mount
●   ├─snap-gnome\x2d46\x2d2404-153.mount
●   ├─snap-gtk\x2dcommon\x2dthemes-1535.mount
●   ├─snap-mesa\x2d2404-1165.mount
●   ├─snap-snap\x2dstore-1270.mount
●   ├─snap-snapd-25935.mount
●   ├─snap-snapd\x2ddesktop\x2dintegration-343.mount
●   ├─snap-telegram\x2ddesktop-6899.mount
●   ├─snapd.apparmor.service
○   ├─snapd.autoimport.service
○   ├─snapd.core-fixup.service
○   ├─snapd.recovery-chooser-trigger.service
●   ├─snapd.seeded.service
●   ├─snapd.service
○   ├─ssl-cert.service
○   ├─sssd.service
●   ├─sysstat.service
●   ├─systemd-ask-password-wall.path
●   ├─systemd-logind.service
●   ├─systemd-oomd.service
○   ├─systemd-update-utmp-runlevel.service
●   ├─systemd-user-sessions.service
○   ├─thermald.service
○   ├─ua-reboot-cmds.service
○   ├─ubuntu-advantage.service
●   ├─ufw.service
●   ├─unattended-upgrades.service
●   ├─whoopsie.path
●   ├─wpa_supplicant.service
●   ├─basic.target
●   │ ├─-.mount
○   │ ├─tmp.mount
●   │ ├─paths.target
○   │ │ ├─apport-autoreport.path
○   │ │ └─tpm-udev.path
●   │ ├─slices.target
●   │ │ ├─-.slice
●   │ │ └─system.slice
●   │ ├─sockets.target
○   │ │ ├─apport-forward.socket
●   │ │ ├─avahi-daemon.socket
●   │ │ ├─cups.socket
●   │ │ ├─dbus.socket
●   │ │ ├─snapd.socket
●   │ │ ├─systemd-initctl.socket
●   │ │ ├─systemd-journald-dev-log.socket
●   │ │ ├─systemd-journald.socket
●   │ │ ├─systemd-oomd.socket
○   │ │ ├─systemd-pcrextend.socket
●   │ │ ├─systemd-sysext.socket
●   │ │ ├─systemd-udevd-control.socket
●   │ │ ├─systemd-udevd-kernel.socket
●   │ │ └─uuidd.socket
●   │ ├─sysinit.target
●   │ │ ├─apparmor.service
●   │ │ ├─dev-hugepages.mount
●   │ │ ├─dev-mqueue.mount
●   │ │ ├─keyboard-setup.service
●   │ │ ├─kmod-static-nodes.service
○   │ │ ├─ldconfig.service
●   │ │ ├─plymouth-read-write.service
●   │ │ ├─plymouth-start.service
●   │ │ ├─proc-sys-fs-binfmt_misc.automount
●   │ │ ├─setvtrgb.service
●   │ │ ├─sys-fs-fuse-connections.mount
●   │ │ ├─sys-kernel-config.mount
●   │ │ ├─sys-kernel-debug.mount
●   │ │ ├─sys-kernel-tracing.mount
○   │ │ ├─systemd-ask-password-console.path
●   │ │ ├─systemd-binfmt.service
○   │ │ ├─systemd-firstboot.service
○   │ │ ├─systemd-hwdb-update.service
○   │ │ ├─systemd-journal-catalog-update.service
●   │ │ ├─systemd-journal-flush.service
●   │ │ ├─systemd-journald.service
○   │ │ ├─systemd-machine-id-commit.service
●   │ │ ├─systemd-modules-load.service
○   │ │ ├─systemd-pcrmachine.service
○   │ │ ├─systemd-pcrphase-sysinit.service
○   │ │ ├─systemd-pcrphase.service
○   │ │ ├─systemd-pstore.service
●   │ │ ├─systemd-random-seed.service
○   │ │ ├─systemd-repart.service
●   │ │ ├─systemd-resolved.service
●   │ │ ├─systemd-sysctl.service
○   │ │ ├─systemd-sysusers.service
●   │ │ ├─systemd-timesyncd.service
●   │ │ ├─systemd-tmpfiles-setup-dev-early.service
●   │ │ ├─systemd-tmpfiles-setup-dev.service
●   │ │ ├─systemd-tmpfiles-setup.service
○   │ │ ├─systemd-tpm2-setup-early.service
○   │ │ ├─systemd-tpm2-setup.service
●   │ │ ├─systemd-udev-trigger.service
●   │ │ ├─systemd-udevd.service
○   │ │ ├─systemd-update-done.service
●   │ │ ├─systemd-update-utmp.service
●   │ │ ├─cryptsetup.target
●   │ │ ├─integritysetup.target
●   │ │ ├─local-fs.target
●   │ │ │ ├─-.mount
○   │ │ │ ├─systemd-fsck-root.service
●   │ │ │ └─systemd-remount-fs.service
●   │ │ ├─swap.target
●   │ │ │ └─swap.img.swap
●   │ │ └─veritysetup.target
●   │ └─timers.target
●   │   ├─anacron.timer
○   │   ├─apport-autoreport.timer
●   │   ├─apt-daily-upgrade.timer
●   │   ├─apt-daily.timer
●   │   ├─dpkg-db-backup.timer
●   │   ├─e2scrub_all.timer
●   │   ├─fstrim.timer
●   │   ├─fwupd-refresh.timer
●   │   ├─logrotate.timer
●   │   ├─man-db.timer
●   │   ├─motd-news.timer
○   │   ├─snapd.snap-repair.timer
●   │   ├─systemd-tmpfiles-clean.timer
○   │   ├─ua-timer.timer
●   │   ├─update-notifier-download.timer
●   │   └─update-notifier-motd.timer
●   ├─getty.target
○   │ ├─getty-static.service
○   │ └─getty@tty1.service
●   └─remote-fs.target

maks@maks-VirtualBox:~$ systemctl list-dependencies multi-user.target
multi-user.target
○ ├─anacron.service
● ├─apport.service
● ├─avahi-daemon.service
● ├─console-setup.service
● ├─cron.service
● ├─cups-browsed.service
● ├─cups.path
● ├─cups.service
● ├─dbus.service
○ ├─dmesg.service
○ ├─e2scrub_reap.service
○ ├─grub-common.service
○ ├─grub-initrd-fallback.service
● ├─kerneloops.service
● ├─ModemManager.service
○ ├─networkd-dispatcher.service
● ├─NetworkManager.service
○ ├─open-vm-tools.service
● ├─openvpn.service
● ├─plymouth-quit-wait.service
○ ├─plymouth-quit.service
● ├─rsyslog.service
○ ├─run-vmblock\x2dfuse.mount
○ ├─secureboot-db.service
● ├─snap-bare-5.mount
● ├─snap-core22-2292.mount
● ├─snap-core24-1349.mount
● ├─snap-firefox-7766.mount
● ├─snap-firmware\x2dupdater-210.mount
● ├─snap-gnome\x2d42\x2d2204-247.mount
● ├─snap-gnome\x2d46\x2d2404-153.mount
● ├─snap-gtk\x2dcommon\x2dthemes-1535.mount
● ├─snap-mesa\x2d2404-1165.mount
● ├─snap-snap\x2dstore-1270.mount
● ├─snap-snapd-25935.mount
● ├─snap-snapd\x2ddesktop\x2dintegration-343.mount
● ├─snap-telegram\x2ddesktop-6899.mount
● ├─snapd.apparmor.service
○ ├─snapd.autoimport.service
○ ├─snapd.core-fixup.service
○ ├─snapd.recovery-chooser-trigger.service
● ├─snapd.seeded.service
● ├─snapd.service
○ ├─ssl-cert.service
○ ├─sssd.service
● ├─sysstat.service
● ├─systemd-ask-password-wall.path
● ├─systemd-logind.service
● ├─systemd-oomd.service
○ ├─systemd-update-utmp-runlevel.service
● ├─systemd-user-sessions.service
○ ├─thermald.service
○ ├─ua-reboot-cmds.service
○ ├─ubuntu-advantage.service
● ├─ufw.service
● ├─unattended-upgrades.service
● ├─whoopsie.path
● ├─wpa_supplicant.service
● ├─basic.target
● │ ├─-.mount
○ │ ├─tmp.mount
● │ ├─paths.target
○ │ │ ├─apport-autoreport.path
○ │ │ └─tpm-udev.path
● │ ├─slices.target
● │ │ ├─-.slice
● │ │ └─system.slice
● │ ├─sockets.target
○ │ │ ├─apport-forward.socket
● │ │ ├─avahi-daemon.socket
● │ │ ├─cups.socket
● │ │ ├─dbus.socket
● │ │ ├─snapd.socket
● │ │ ├─systemd-initctl.socket
● │ │ ├─systemd-journald-dev-log.socket
● │ │ ├─systemd-journald.socket
● │ │ ├─systemd-oomd.socket
○ │ │ ├─systemd-pcrextend.socket
● │ │ ├─systemd-sysext.socket
● │ │ ├─systemd-udevd-control.socket
● │ │ ├─systemd-udevd-kernel.socket
● │ │ └─uuidd.socket
● │ ├─sysinit.target
● │ │ ├─apparmor.service
● │ │ ├─dev-hugepages.mount
● │ │ ├─dev-mqueue.mount
● │ │ ├─keyboard-setup.service
● │ │ ├─kmod-static-nodes.service
○ │ │ ├─ldconfig.service
● │ │ ├─plymouth-read-write.service
● │ │ ├─plymouth-start.service
● │ │ ├─proc-sys-fs-binfmt_misc.automount
● │ │ ├─setvtrgb.service
● │ │ ├─sys-fs-fuse-connections.mount
● │ │ ├─sys-kernel-config.mount
● │ │ ├─sys-kernel-debug.mount
● │ │ ├─sys-kernel-tracing.mount
○ │ │ ├─systemd-ask-password-console.path
● │ │ ├─systemd-binfmt.service
○ │ │ ├─systemd-firstboot.service
○ │ │ ├─systemd-hwdb-update.service
○ │ │ ├─systemd-journal-catalog-update.service
● │ │ ├─systemd-journal-flush.service
● │ │ ├─systemd-journald.service
○ │ │ ├─systemd-machine-id-commit.service
● │ │ ├─systemd-modules-load.service
○ │ │ ├─systemd-pcrmachine.service
○ │ │ ├─systemd-pcrphase-sysinit.service
○ │ │ ├─systemd-pcrphase.service
○ │ │ ├─systemd-pstore.service
● │ │ ├─systemd-random-seed.service
○ │ │ ├─systemd-repart.service
● │ │ ├─systemd-resolved.service
● │ │ ├─systemd-sysctl.service
○ │ │ ├─systemd-sysusers.service
● │ │ ├─systemd-timesyncd.service
● │ │ ├─systemd-tmpfiles-setup-dev-early.service
● │ │ ├─systemd-tmpfiles-setup-dev.service
● │ │ ├─systemd-tmpfiles-setup.service
○ │ │ ├─systemd-tpm2-setup-early.service
○ │ │ ├─systemd-tpm2-setup.service
● │ │ ├─systemd-udev-trigger.service
● │ │ ├─systemd-udevd.service
○ │ │ ├─systemd-update-done.service
● │ │ ├─systemd-update-utmp.service
● │ │ ├─cryptsetup.target
● │ │ ├─integritysetup.target
● │ │ ├─local-fs.target
● │ │ │ ├─-.mount
○ │ │ │ ├─systemd-fsck-root.service
● │ │ │ └─systemd-remount-fs.service
● │ │ ├─swap.target
● │ │ │ └─swap.img.swap
● │ │ └─veritysetup.target
● │ └─timers.target
● │   ├─anacron.timer
○ │   ├─apport-autoreport.timer
● │   ├─apt-daily-upgrade.timer
● │   ├─apt-daily.timer
● │   ├─dpkg-db-backup.timer
● │   ├─e2scrub_all.timer
● │   ├─fstrim.timer
● │   ├─fwupd-refresh.timer
● │   ├─logrotate.timer
● │   ├─man-db.timer
● │   ├─motd-news.timer
○ │   ├─snapd.snap-repair.timer
● │   ├─systemd-tmpfiles-clean.timer
○ │   ├─ua-timer.timer
● │   ├─update-notifier-download.timer
● │   └─update-notifier-motd.timer
● ├─getty.target
○ │ ├─getty-static.service
○ │ └─getty@tty1.service
● └─remote-fs.target
```

### **Task 1.4 — User Sessions**

1. Audit Login Activity

```bash
maks@maks-VirtualBox:~$ who -a
           system boot  2026-02-27 23:09
maks     ? seat0        2026-02-27 23:09   ?          1300 (login screen)
maks     + tty2         2026-02-27 23:09 00:06        1300 (tty2)
           run-level 5  2026-02-27 23:09

maks@maks-VirtualBox:~$ last -n 5
maks     tty2         tty2             Fri Feb 27 23:09   still logged in
maks     seat0        login screen     Fri Feb 27 23:09   still logged in
reboot   system boot  6.17.0-14-generi Fri Feb 27 23:09   still running
maks     tty2         tty2             Fri Feb 27 22:12 - crash  (00:57)
maks     seat0        login screen     Fri Feb 27 22:12 - crash  (00:57)

wtmp begins Fri Feb 27 21:57:05 2026
```

### **Task 1.5 — Memory Analysis**

1. Inspect Memory Allocation

```bash
maks@maks-VirtualBox:~$ free -h
               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       2.3Gi       143Mi        69Mi       1.7Gi       1.6Gi
Swap:          2.4Gi       262Mi       2.1Gi

maks@maks-VirtualBox:~$ cat /proc/meminfo | grep -e MemTotal -e SwapTotal -e MemAvailable
MemTotal:        4007368 kB
MemAvailable:    1635252 kB
SwapTotal:       2510844 kB
```

### **Key Observations for Sections**

1.1) The total load time is `36.1 s`
    The slowest service: `plymouth-quit-wait.service`
    According to the load average `(1.0-1.2 s)`, the system is not overloaded

1.2) GUI applications consume a lot of resources

1.3) `default.target` depends on graphical services and `multi-user.target` depends on a lot of network services

1.4) I (the `maks` user) work have been working since 23:09 via `ttu2`, and the previous session that started at 22:12 have crashed

1.5) RAM: `3.8 GiB` at total, consumed `2.3 GiB`. SWAP: `262 MiB` of `2.4 GiB` are used that is not critical for the swap memory.

### **Top Memory-Consuming Process**

The top memory-cosuming process is `/snap/snap-store/1270/bin/s` (`PID 4132`), consuming `13.1%` of total memory.

### **Resource Utilization Patterns**

Overall, resources are distributed unevenly: the main "heavyweights" are user applications, while background services (especially Snap) create a constant, but low, load.


## **Task 2 — Networking Analysis**

### **Task 2.1 — Network Path Tracing**

1. Traceroute Execution

```bash
maks@maks-VirtualBox:~$ traceroute github.com
traceroute to github.com (140.82.121.4), 30 hops max, 60 byte packets
 1  _gateway (10.0.2.2)  12.388 ms  11.341 ms  0.569 ms
 2  * * *
 3  * * *
 4  * * *
 5  * * *
 6  * * *
 7  * * *
 8  * * *
 9  * * *
10  * * *
11  * * *
12  * * *
13  * * *
14  * * *
15  * * *
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  * * *
22  * * *
23  * * *
24  * * *
25  * * *
26  * * *
27  * * *
28  * * *
29  * * *
30  * * *
```

2. DNS Resolution Check

```bash
maks@maks-VirtualBox:~$ dig github.com

; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> github.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 28016
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;github.com.			IN	A

;; ANSWER SECTION:
github.com.		8	IN	A	140.82.121.4

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Fri Feb 27 22:47:03 MSK 2026
;; MSG SIZE  rcvd: 55
```

### **Task 2.2 — Packet Capture**

1. Capture DNS Traffic

```bash
maks@maks-VirtualBox:~$ sudo timeout 10 tcpdump -c 5 -i any 'port 53' -nn

tcpdump: data link type LINUX_SLL2
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on any, link-type LINUX_SLL2 (Linux cooked v2), snapshot length 262144 bytes
23:48:05.204558 lo    In  IP 127.0.0.1.57384 > 127.0.0.53.53: 23671+ [1au] A? ipv4only.arpa. (42)
23:48:05.205809 lo    In  IP 127.0.0.1.57384 > 127.0.0.53.53: 27465+ [1au] AAAA? ipv4only.arpa. (42)
23:48:05.205932 lo    In  IP 127.0.0.53.53 > 127.0.0.1.57384: 23671 2/0/1 A 192.0.0.171, A 192.0.0.170 (74)
23:48:05.206813 enp0s3 Out IP 10.0.2.15.49689 > 192.168.0.1.53: 42295+ [1au] AAAA? ipv4only.arpa. (42)
23:48:05.214709 enp0s3 In  IP 192.168.0.1.53 > 10.0.2.15.49689: 42295 0/1/1 (99)
5 packets captured
10 packets received by filter
0 packets dropped by kernel
```

### **Task 2.3 — Reverse DNS**

1. PTR Lookups

```bash
maks@maks-VirtualBox:~$ dig -x 8.8.4.4

; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> -x 8.8.4.4
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 50999
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;4.4.8.8.in-addr.arpa.		IN	PTR

;; ANSWER SECTION:
4.4.8.8.in-addr.arpa.	5965	IN	PTR	dns.google.

;; Query time: 39 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Fri Feb 27 22:48:24 MSK 2026
;; MSG SIZE  rcvd: 73
```

```bash
maks@maks-VirtualBox:~$ dig -x 1.1.2.2

; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> -x 1.1.2.2
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 59579
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;2.2.1.1.in-addr.arpa.		IN	PTR

;; AUTHORITY SECTION:
1.in-addr.arpa.		765	IN	SOA	ns.apnic.net. read-txt-record-of-zone-first-dns-admin.apnic.net. 23597 7200 1800 604800 3600

;; Query time: 2136 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Fri Feb 27 22:48:41 MSK 2026
;; MSG SIZE  rcvd: 137
```

### **Insights on Network Paths**

The traceroute to `github.com` shows only the first hop with low latency, while all subsequent nodes are unresponsive.

### **Analysis of DNS Query/Response Patterns**

The reverse request for `8.8.4.4` took `39 ms` (successful response), for `1.1.2.2` - `2136 ms` (NXDOMAIN response), which reflects delays in accessing authoritative servers. DNS traffic on port 53 was not captured by tcpdump.

### **Comparison of Reverse Lookup Results**

1) 8.8.4.4: successful PTR resolution -> dns.google

2) 1.1.2.2: response: NXDOMAIN (record missing). This is expected for an address without a reverse zone. The response time is significantly longer due to the root zone queries (1.in-addr.arpa)

### **DNS Query Example**

```bash
23:48:05.204558 lo    In  IP 127.0.0.1.57384 > 127.0.0.53.53: 23671+ [1au] A? ipv4only.arpa. (42)
```
