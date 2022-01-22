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

