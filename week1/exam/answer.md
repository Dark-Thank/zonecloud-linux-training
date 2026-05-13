PhanB.10.b 
sysadmin_test@khanh-GF63-Thin-11UD:~$  touch /opt/zonecloud-exam/scripts/test.txt
touch: cannot touch '/opt/zonecloud-exam/scripts/test.txt': Permission denied
sysadmin_test@khanh-GF63-Thin-11UD:~$ ls -ld /opt/zonecloud-exam/scripts
drwxr-xr-x 2 root root 4096 May 13 21:59 /opt/zonecloud-exam/scripts

Tạo file không được vì /opt/zonecloud-exam/scripts chỉ có root có quyền ghi và group và others chỉ có r-x còn sysadmin_test không phải owner nên không được tạo file 

