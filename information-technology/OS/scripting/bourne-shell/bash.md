### Mounting/Unmounting
#### Mount

- If you get an unexplained error when mounting samba (smb) targets, try to add `vers=1.0` at the end of your directive. It forces the system to use samba v1 to establish connection. Beware it is not safe though, you might wanna apply a firmware update on the server machine.

##### Mount all from fstab
```
# -v is for verbose
# -a is for all 
# it will scan  /etc/fstab and mount all those defined in there
# Depending on the situtation you might have to provide sudo for it to run
mount -av 
```

##### Mount single time from console 
```
# This is for mounting a NAS
sudo mount.cifs //10.18.22.44/some-path/somesubdir /mnt/this-is/where-to-mount/your-external-target -o user=john,password=doe,vers=1.0 0 0
```



#### Unmount
```
# you have to provide the [LOCATION of the mount point] or [drive partition name]
# Depending on the situtation you might have to provide sudo for it to run
unmount /media/my/predefined/mount/point
```







### Unload module
```
rmmod nvidia_uvm
```

### Load module
```
modprobe nvidia_uvm
```


If you change hostname during installation or at some weird point, it may cause delay when issuing ```sudo``` on bash. Especially for starship shell. To fix this edit ```/etc/hosts```.

### Slow when `sudo` issued
- It could be due to hostname change. ```/etc/hosts```. Starship also suffers from this sometimes.


### Execute command on terminal start (e.g open new terminal)
add the command to the end of the ```.bashrc```
```
nano ~/.bashrc
```



### Move folder content to upper level

```
# Case:
.
├── dir1
│   ├── QWE.md
│   └── dir2
│       ├── ABC.md
│       └──  XYZ.md
```

```
# And you want to move content of dir2 to upper level (inside dir1)
.
├── dir1
│   ├── QWE.md
│   └── ABC.md
│   └── XYZ.md
|   └── dir2
```

```
# While inside dir1:

mv dir2/* .

# or change /* to /.*
```


### Command history
```
history
```


### Unfreeze SSH session (terminate connection)
```
1. Enter
2. ~ (tilde)
3. . (period)
```

### Block WiFi adapter
```
#sudo apt install rfkill
sudo rfkill block wifi
#or any other adapter, such as bluetooth
```


### Wipe buggy flash/usb drive
```
wipefs -a /dev/your-device 

```
```
sudo dd if=/dev/zero of=/dev/the-buggy-drive bs=2048 count=32
```

### mkdir with child
```
mkdir -p 
```

### Delete dir
```
rmdir yourDir
```

If has child

```
rm -r yourDir
```

### Disable all connection except LAN (disable internet)
```
 sudo route del default gw 192.168.1.1

 # To re-enable it:
 sudo route add default gw 192.168.1.1
``` 
```
 # Alternative, assumning your LAN range is 192.168.1.0 with /24 (haven't tried)
 iptables -P INPUT DROP
 iptables -A INPUT -s 192.168.1.0/24 -j ACCEPT
```
 
 


### Find your network gateway
```
route -n|grep "^0.0.0.0"
```

### save cd path for shorthand
```
#Add this to bashrc
shopt -s cdable_vars
export myFold=$HOME/Files/Scripts/Main

#So that you can
cd myFold
```

### Reload .bashrc
```
source ~/.bashrc
```

### Local ip in the network
```
hostname -I
```

### Kill webstorm or phpstorm
```
kill -9 $(pgrep -f webstorm)
```

### Suspend job, send to background
```
ctrl + z
```

### Background jobs
```
jobs
```


### Switch back to the job
```
# "1" is the number that is displayed after using jobs comm.
bg %1 
```

### Bring to foreground
```
fg %1
```

