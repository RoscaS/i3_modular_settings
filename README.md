* [Alternatives système pour i3](https://www.reddit.com/r/i3wm/comments/6txwcz/light_desktop_environment_to_use_i3_on/)


## Problème de hotplugg (monitor)
Dans le fichier conf de i3:
`exec --no-startup-id compton #Gestion transparence`

Dans `~/.config/compton.config`

```
backend = "glx"
mark-wmwin-focused = true;
mark-ovredir-focused = true;
detect-rounded-corners = true;
detect-client-opacity = true;
refresh-rate = 0;
vsync = "none";
dbe = false;
paint-on-overlay = true;
detect-transient = true;
detect-client-leader = true;
glx-no-stencil = true;
glx-copy-from-front = false;
glx-no-rebind-pixmap = true;
glx-swap-method = 3;
```

### Autodetect (monitor plugged-in)
https://github.com/wertarbyte/autorandr


## Changement de layout (clavier)
> Pas permanent pour le moment.

Comme d'habitude pour le layout (voir repo layout so_linux).

Pour set le layout (permanent): `localectl set-x11-keymap so` 

Dans `~/.conf/Xmodmap`:

```
remove Mod1 = Alt_R
keycode 108 = Alt_R
```

Ensuite `xmodmap ~/.Xmodmap`
Et `xmodmap -e "keycode 108 = ISO_Level3_Shift"`

### Commandes utiles

Pour set le nouveau language: `localectl set-x11-keymap so` 
Verifier le langage utilisé: `setxkbmap -query`

Afficher tous les keycodes: `xmodmap -pke`
Affiche en temps réel des infos sur l'input `xev`


## Power management

Utils:
* tlp
* autosuspend

### Bluetooth
* bluez
* bluez-tools
* blueman

`$ gsettings set org.blueman.plugins.powermanager auto-power-on false`


### Comportement lid close
Tout est là `/etc/systemd/logind.conf`

#### En cas de soucis de behave du "suspend" state

* [infos](https://wiki.archlinux.org/index.php/Power_management#Power_management_with_systemd)

```
/etc/systemd/sleep.conf

[Sleep]
# suspend=hybrid-sleep
SuspendMode=suspend
SuspendState=disk
# hibernate=hybrid-sleep
HibernateMode=suspend
HibernateState=disk
```

### Huge cursor
dans `.Xressources`: `Xcursor.size: 16`

## Rice

* ranger

### .Xressources

`~/.Xressources`

```
rofi.color-enabled: true
rofi.color-window: #141021, #c16772, #9568a1
rofi.color-normal: #141021, #ffeefc, #312842, #c16772, #ffeefc
rofi.color-active: #141021, #c05c47, #312842, #c05c47, #ffeefc
rofi.color-urgent: #141021, #e4b226, #312842, #e4b226, #ffeefc
rofi.width: 800
rofi.padding: 50
rofi.font: PragmataPro Nerd Font 18
rofi.bw: 3
rofi.separator-style: solid
rofi.hide-scrollbar: true
```

### Lock

*[i3lock-multimonitor](https://github.com/guimeira/i3lock-fancy-multimonitor)

#### Lock before sleep

create `/etc/systemd/system/i3lock@.service`
append:

```
[Unit]
Description=i3lock
Before=sleep.target

[Service]
User=<username>
Type=forking
Environment=DISPLAY=:0
ExecStart=<path_to_i3lock>

[Install]
WantedBy=sleep.target
```

enable `systemctl enable i3lock@username.service`
check `systemctl status i3lock@username.service`


### npd (Music_Player_Daemon)

* [tuto](https://computingforgeeks.com/how-to-configure-mpd-and-ncmpcpp-on-linux/)
* [doc npd](https://wiki.archlinux.org/index.php/Music_Player_Daemon)
  *  [en cas de soucis avec le socket](https://bbs.archlinux.org/viewtopic.php?id=120371)


### ncmpcpp
* [doc](https://wiki.archlinux.org/index.php/ncmpcpp)

* `1` - Current playlist
* `2` - Filesystem browser
* `3` - DB search
* `4` - Library
* `5` - Playlist editor
* `6` - Tag editor (very powerful!)
* `7` - Output selector
* `8` - Music visualizer
* `=` - Clock
* `F1` - Help


* `q` - Quit
* `f` - Seek forward
* `b` - Seek backward
* `\` - Switch between classic and alternative views
* `#` - Display bitrate of file
* `i` - Show song info
* `I` - Show artist info (saved in ~/.ncmpcpp/artists/ARTIST.txt)
* `L` - Shuffle between available lyric databases
* `l` - Retrieve song lyrics for current song Show/hide lyrics
* `>` - Next track
* `<` - Previous track
* `p` - Play/Pause
* `+` - Increase volume 2%
* `-` - Decrease volume 2%


### modipy

* [register](https://www.mopidy.com/authenticate/#spotify)

### Terminator

`~/.config/terminator/config`

```
[global_config]
  borderless = True
  enabled_plugins = LaunchpadCodeURLHandler, APTURLHandler, LaunchpadBugURLHandler
  suppress_multiple_term_dialog = True
[keybindings]
  broadcast_off = <Alt>q
  cycle_next = <Alt>0
  cycle_prev = <Alt>9
  hide_window = <Primary>grave
[layouts]
  [[default]]
    [[[child0]]]
      fullscreen = False
      last_active_term = 876fc29d-0f85-4b80-a874-952a84168288
      last_active_window = True
      maximised = False
      order = 0
      parent = ""
      position = 2084:876
      size = 837, 704
      title = sol@sol-XPS13: ~/Code/Web/01-Generic_website/project
      type = Window
    [[[terminal1]]]
      order = 0
      parent = child0
      profile = default
      type = Terminal
      uuid = 876fc29d-0f85-4b80-a874-952a84168288
  [[generic_website]]
    [[[child0]]]
      fullscreen = False
      last_active_term = 88ae566c-67d8-4da2-9c23-7527aca10ad5
      last_active_window = True
      maximised = False
      order = 0
      parent = ""
      position = 2084:306
      size = 573, 1274
      title = sol@sol-XPS13: ~/Code/Web/01-Generic_website/project
      type = Window
    [[[child1]]]
      order = 0
      parent = child0
      position = 794
      ratio = 0.625196232339
      type = VPaned
    [[[child2]]]
      order = 0
      parent = child1
      position = 90
      ratio = 0.116498740554
      type = VPaned
    [[[terminal3]]]
      directory = /home/sol/Code/Web/01-Generic_website/project
      order = 0
      parent = child2
      profile = default
      type = Terminal
      uuid = 876fc29d-0f85-4b80-a874-952a84168288
    [[[terminal4]]]
      directory = /home/sol/Code/Web/01-Generic_website/project
      order = 1
      parent = child2
      profile = default
      type = Terminal
      uuid = 88ae566c-67d8-4da2-9c23-7527aca10ad5
    [[[terminal5]]]
      directory = /home/sol/Code/Web/01-Generic_website/project
      order = 1
      parent = child1
      profile = default
      type = Terminal
      uuid = bf97c7ca-4279-451f-821f-88b9fb5b3e8e
[plugins]
  [[EditorPlugin]]
    command = gvim --remote-silent +{line} {filepath}
    groups = file line
    match = ([^ \t\n\r\f\v:]+?):([0-9]+)
[profiles]
  [[default]]
    background_color = "#2f3136"
    background_darkness = 0.92
    background_type = transparent
    copy_on_selection = True
    cursor_color = "#edea19"
    cursor_shape = ibeam
    custom_command = TERM=xterm-256color zsh -l
    font = PragmataPro 13
    foreground_color = "#f3f3f3"
    palette = "#212121:#b7141f:#457b24:#f6981e:#134eb2:#560088:#1398a7:#efefef:#424242:#e83b3f:#7aba3a:#ffea2e:#54a4f3:#aa4dbc:#26bbd1:#d9d9d9"
    scrollback_infinite = True
    scrollbar_position = hidden
    show_titlebar = False
    use_custom_command = True
    use_system_font = False
  [[clear]]
    background_color = "#2f3136"
    background_darkness = 0.0
    background_type = transparent
    copy_on_selection = True
    cursor_color = "#edea19"
    cursor_shape = ibeam
    font = PragmataPro 17
    foreground_color = "#babdb6"
    palette = "#212121:#b7141f:#457b24:#f6981e:#134eb2:#560088:#0e717c:#efefef:#424242:#e83b3f:#7aba3a:#ffea2e:#54a4f3:#aa4dbc:#26bbd1:#d9d9d9"
    scrollback_infinite = True
    scrollbar_position = hidden
    show_titlebar = False
    use_system_font = False
  [[sol]]
    cursor_color = "#aaaaaa"
```


`~/config/gtk-3.0/gtk.css`

```css
VteTerminal, vte-terminal {
  padding-top: 20px;
  padding-bottom: 20px;
  padding-left: 20px;
  padding-right: 20px;
}
```

