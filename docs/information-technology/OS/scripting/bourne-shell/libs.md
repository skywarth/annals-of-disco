## JQ (reading JSON)
```
constants=$(cat "test.json" | jq '.' | jq -r "to_entries|map(\"\(.key)=\(.value|tostring)\")|.[]")
echo $constants
exit

```

Alternative
```

  {
	"SITE_DATA": {
	  "URL": "example.com",
	  "AUTHOR": "John Doe",
	  "CREATED": "10/22/2017"
	}
  }
  # If you wan't every attribute inside SITE_DATA:
  typeset -A myarray

while IFS== read -r key value; do
    myarray["$key"]="$value"
done < <(jq -r '.SITE_DATA | to_entries | .[] | .key + "=" + .value ' test2.json)


# make use of the array variables
echo "URL = '${myarray[URL]}'"
echo "CREATED = '${myarray[CREATED]}'"
echo "AUTHOR = '${myarray[AUTHOR]}'"
```

Full recursive, but you cannot use any integer at all
```
SOURCE="$PWD"
SETTINGS_FILE="./test2.json"
SETTINGS_JSON=`cat "$SETTINGS_FILE"`

declare -A SETTINGS

get_settings() {
    local PARAMS="$#"
    local JSON=`jq -r "to_entries|map(\"\(.key)=\(.value|tostring)\")|.[]" <<< "$1"`
    local KEYS=''

    if [ $# -gt 1 ]; then
        KEYS="$2"
    fi

    while read -r PAIR; do
        local KEY=''

        if [ -z "$PAIR" ]; then
            break
        fi

        IFS== read PAIR_KEY PAIR_VALUE <<< "$PAIR"

        if [ -z "$KEYS" ]; then
            KEY="$PAIR_KEY"
        else
            KEY="$KEYS:$PAIR_KEY"
        fi

        if jq -e . >/dev/null 2>&1 <<< "$PAIR_VALUE"; then
            get_settings "$PAIR_VALUE" "$KEY"
        else
            SETTINGS["$KEY"]="$PAIR_VALUE"
        fi
    done <<< "$JSON"
}
```


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

- Tmux-powerline (plugin, not the font) [https://github.com/erikw/tmux-powerline]

If your tmux status bar icons looks slightly offset, like they have some margin: adjust your font and it's size to fit.


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
