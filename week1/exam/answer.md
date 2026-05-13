PhanB.10.b 
sysadmin_test@khanh-GF63-Thin-11UD:~$  touch /opt/zonecloud-exam/scripts/test.txt
touch: cannot touch '/opt/zonecloud-exam/scripts/test.txt': Permission denied
sysadmin_test@khanh-GF63-Thin-11UD:~$ ls -ld /opt/zonecloud-exam/scripts
drwxr-xr-x 2 root root 4096 May 13 21:59 /opt/zonecloud-exam/scripts

Tạo file không được vì /opt/zonecloud-exam/scripts chỉ có root có quyền ghi và group và others chỉ có r-x còn sysadmin_test không phải owner nên không được tạo file 




PhanC.13 
khanh@khanh-GF63-Thin-11UD:/media/khanh/Disk/ZoneCloudTraining/zonecloud-linux-training$ ps aux --sort=-%mem | head -5
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
khanh       5622  8.0  9.0 1518888344 708052 ?   Sl   16:51  26:31 /opt/google/chrome/chrome --type=renderer --crashpad-handler-pid=2278 --enable-crash-reporter=ba064c32-f8a2-4cef-8f6c-ef2eb89298e7, --change-stack-guard-on-fork=enable --ozone-platform=x11 --lang=en-US --num-raster-threads=4 --enable-main-frame-before-activation --renderer-client-id=24 --time-ticks-at-unix-epoch=-1778660655611273 --launch-time-ticks=5249100933 --shared-files=v8_context_snapshot_data:100 --metrics-shmem-handle=4,i,9566539281050032685,16102790124420721958,2097152 --field-trial-handle=3,i,9738542575497838714,5570560929401946500,262144 --variations-seed-version=20260512-170052.558000-production --pseudonymization-salt-handle=7,i,13673936260947665810,7208334717957191504,4 --trace-process-track-uuid=3190709008800875870
khanh       2270  1.4  6.1 51452908 479204 ?     SLl  15:25   5:50 /opt/google/chrome/chrome
khanh       1941  0.1  5.9 1155244 465300 ?      Sl   15:24   0:30 /home/khanh/Downloads/Telegram/Telegram
khanh       2205  0.3  4.9 1427804 386892 ?      Sl   15:25   1:39 /usr/lib/libreoffice/program/soffice.bin --writer file:///media/khanh/Disk/ZoneCloudTraining/sysadmin-training-week1.txt --splash-pipe=5
khanh@khanh-GF63-Thin-11UD:/media/khanh/Disk/ZoneCloudTraining/zonecloud-linux-training$ 

==> ps aux nghĩa là hiển thị toàn bộ process 
"--sort=-%mem" nghĩa là sắp xếp giảm dần theo RAM sử dụng 
head 5 nghĩa là lấy 5 dòng đầu 
/opt/google/chrome/chrome đang dùng RAM nhiều nhất vì đứng top đầu với thông số %MEM = 9.0 


PhanC.14
top - 22:28:14 up  7:03,  1 user,  load average: 0,36, 0,36, 0,43
Tasks: 333 total,   1 running, 332 sleeping,   0 stopped,   0 zombie
%Cpu(s):  1,9 us,  0,7 sy,  0,0 ni, 97,0 id,  0,4 wa,  0,0 hi,  0,0 si,  0,0 st 
MiB Mem :   7642,1 total,   1786,1 free,   3442,5 used,   3153,9 buff/cache     
MiB Swap:      0,0 total,      0,0 free,      0,0 used.   4199,6 avail Mem 

==> load average có 0.36, 0.36, 0.43 
Ba số này là mức tải trung bình của hệ thống trong
-- số thứ nhất 0.15 -> 1 phút gần nhất 
-- số thứ hai -> 5 phút gần nhất 
-- số thứ ba -> 15 phút gần nhất 
==> Máy đăng chỉ sử đụng khoảng 36% hiệu năng và điều giữ ổn định trong 15 phút  


PhanC.15 
khanh@khanh-GF63-Thin-11UD:/media/khanh/Disk/ZoneCloudTraining/zonecloud-linux-training$ systemctl list-units --type=service --state=running
  UNIT                          LOAD   ACTIVE SUB     DESCRIPTION                                                     
  accounts-daemon.service       loaded active running Accounts Service
  avahi-daemon.service          loaded active running Avahi mDNS/DNS-SD Stack
  bluetooth.service             loaded active running Bluetooth service
  colord.service                loaded active running Manage, Install and Generate Color Profiles
  cron.service                  loaded active running Regular background program processing daemon
  cups-browsed.service          loaded active running Make remote CUPS printers available locally
  cups.service                  loaded active running CUPS Scheduler
  dbus.service                  loaded active running D-Bus System Message Bus
  fwupd.service                 loaded active running Firmware update daemon
  getty@tty1.service            loaded active running Getty on tty1
  irqbalance.service            loaded active running irqbalance daemon
  kerneloops.service            loaded active running Tool to automatically collect and submit kernel crash signatures
  lightdm.service               loaded active running Light Display Manager
  ModemManager.service          loaded active running Modem Manager
  NetworkManager.service        loaded active running Network Manager
  nginx.service                 loaded active running A high performance web server and a reverse proxy server
  polkit.service                loaded active running Authorization Manager
  power-profiles-daemon.service loaded active running Power Profiles daemon
  rsyslog.service               loaded active running System Logging Service
  rtkit-daemon.service          loaded active running RealtimeKit Scheduling Policy Service
  ssh.service                   loaded active running OpenBSD Secure Shell server
  switcheroo-control.service    loaded active running Switcheroo Control Proxy service
  systemd-journald.service      loaded active running Journal Service
  systemd-logind.service        loaded active running User Login Management
  systemd-resolved.service      loaded active running Network Name Resolution
  systemd-timesyncd.service     loaded active running Network Time Synchronization
  systemd-udevd.service         loaded active running Rule-based Manager for Device Events and Files
  thermald.service              loaded active running Thermal Daemon Service
  touchegg.service              loaded active running Touchégg Daemon
  udisks2.service               loaded active running Disk Manager
  upower.service                loaded active running Daemon for power management
  user@1000.service             loaded active running User Manager for UID 1000
  wpa_supplicant.service        loaded active running WPA supplicant

Legend: LOAD   → Reflects whether the unit definition was properly loaded.
        ACTIVE → The high-level unit activation state, i.e. generalization of SUB.
        SUB    → The low-level unit activation state, values depend on unit type.

33 loaded units listed.

==> Cho thầy được 33 service đang chạy 



PhanD.18 
- ps aux
  Hiển thị tất cả process đang chạy trên hệ thống.

- grep nginx
  Lọc ra các process có chứa chữ "nginx".

- grep -v grep
  Loại bỏ process grep khỏi kết quả.

- awk '{print $2, $11}'
  In ra:
  + $2  → PID của process
  + $11 → tên command/process


PhanD.19 
453M	/var/lib
214M	/var/cache
185M	/var/log
13M	/var/backups
48K	/var/tmp
48K	/var/spool
12K	/var/www
4,0K	/var/opt
4,0K	/var/mail
4,0K	/var/local
0	/var/run
0	/var/lock
==> 453M /var/lib là thư mục lớn nhất trong /var



