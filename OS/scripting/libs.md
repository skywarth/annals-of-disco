## Rename file names starting with x to starting with y
```
rename 's/X/Y/g' *
```

## Nload
*Is for network load tracking*

## Speedtest-cli

## Nano
```
- Alt - U Undo
- Alt + ^ Copy
- Ctrl + K Cut (use this)
- Ctrl + U Paste
```
## Tmux
*This one is pretty decent config:*

https://github.com/gpakosz/.tmux#configuration

```
- <prefix> c Create a new window
- <prefix> w Choose window from a list
- <prefix> - splits the current pane vertically
- <prefix> _ splits the current pane horizontally
- <prefix> h, <prefix> j, <prefix> k and <prefix> l let you navigate panes ala Vim
- <prefix> x Close the current pan
- <prefix> Enter enters copy-mode
- <prefix> space begin selection
- y or use the damn mouse
```

*Also needs the following stuff*

- Tmux plugin manager
```
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```
*then add this to end of the config:*
```
# List of plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'

# Other examples:
# set -g @plugin 'github_username/plugin_name'
# set -g @plugin 'git@github.com:user/plugin'
# set -g @plugin 'git@bitbucket.com:user/plugin'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'
```
- Tmux yank
*Add to config* ```set -g @plugin 'tmux-plugins/tmux-yank'```
```prefix–I install tmux-yank```
- Xsel 
```sudo apt-get install xsel # or xclip```




---

## Get pressed key code
```
sudo apt-get install showkey
sudo showkey
```
---

## Screen
*Case sensitive*
- ```Ctrl+a c```  Create a new window
- ```Ctrl+a A Rename``` the current window
- ```Ctrl+a "``` List all window
- ```Ctrl+k "``` Kill current window
- ```Ctrl+a S``` Split current region horizontally into two regions
- ```Ctrl+a |``` Split current region vertically into two regions
- ```Ctrl+a tab``` Switch the input focus to the next region

---
