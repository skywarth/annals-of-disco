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

