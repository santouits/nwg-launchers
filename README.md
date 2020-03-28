# nwg-launchers
As it's never too late to learn something new, I decided to try and code my 
[sgtk-menu](https://github.com/nwg-piotr/sgtk-menu) set of launchers, written in python, from scratch in C++.
By the way I'm trying to simplify their usage, by reducing the number of arguments. Whatever possible, is being moved
to css style sheets.

It's damned difficult to make all the stuff behave properly on all window managers. My priorities are:

1. it **must work well** on sway;
2. it **should work as well as possible** on i3 and Openbox.

Feel free to report issues you encounter on other window managers / desktop environments, but they may or may not be resolved.

For now first three launchers seem to work pretty well, at least on Arch Linux:

# nwggrid

This command creates a GNOME-like application grid, with the search box, optionally prepended with a row of favourites
(most frequently used apps).

[![Swappshot-Mon-Mar-23-205030-2020.th.png](https://scrot.cloud/images/2020/03/23/Swappshot-Mon-Mar-23-205030-2020.th.png)](https://scrot.cloud/image/jb3k) [![Swappshot-Mon-Mar-23-205157-2020.th.png](https://scrot.cloud/images/2020/03/23/Swappshot-Mon-Mar-23-205157-2020.th.png)](https://scrot.cloud/image/jOWg) [![Swappshot-Mon-Mar-23-205248-2020.th.png](https://scrot.cloud/images/2020/03/23/Swappshot-Mon-Mar-23-205248-2020.th.png)](https://scrot.cloud/image/joh5)

### Dependencies

- `gtkmm3` (`libgtkmm-3.0-dev`)
- `nlohmann-json`

### Installation

```
git clone https://github.com/nwg-piotr/nwg-launchers.git
cd nwg-launchers/grid
sudo make clean install
```
To uninstall:

```
sudo make uninstall
```

### Usage

```
$ nwggrid -h
GTK application grid: nwggrid 0.0.1 (c) Piotr Miller 2020

nwggrid [-h] [-f] [-o <opacity>] [-c <col>] [-s <size>] [-l <ln>]

Options:
-h            show this help message and exit
-f            display favourites
-o <opacity>  background opacity (0.0 - 1.0, default 0.9)
-c <col>      number of grid columns (default: 6)
-s <size>     button image size (default: 72)
-l <ln>       force use of <ln> language
```

### Custom styling

On first run the program creates the `nwgbar` folder in your .config directory. You'll find the `style.css` files inside.
You may edit the style sheet to your liking.

# nwgbar

This command creates a horizontal or vertical button bar, out of a template file.

[![Swappshot-Mon-Mar-23-210713-2020.th.png](https://scrot.cloud/images/2020/03/23/Swappshot-Mon-Mar-23-210713-2020.th.png)](https://scrot.cloud/image/jRPQ) [![Swappshot-Mon-Mar-23-210652-2020.th.png](https://scrot.cloud/images/2020/03/23/Swappshot-Mon-Mar-23-210652-2020.th.png)](https://scrot.cloud/image/j8LU)

### Dependencies

- as above

### Installation

```
git clone https://github.com/nwg-piotr/nwg-launchers.git
cd nwg-launchers/bar
sudo make clean install
```
To uninstall:

```
sudo make uninstall
```

### Usage

```
$ nwgbar -h
GTK button bar: nwgbar 0.0.1 (c) Piotr Miller 2020

nwgbar [-h] [-v] [-ha <l>|<r>] [-va <t>|<b>] [-t <name>] [-o <opacity>] [-s <size>]

Options:
-h            show this help message and exit
-v            arrange buttons vertically
-ha <l>|<r>   horizontal alignment left/right (default: center)
-va <t>|<b>   vertical alignment top/bottom (default: middle)
-t <name>     template file name (default: bar.json)
-o <opacity>  background opacity (0.0 - 1.0, default 0.9)
-s <size>     button image size (default: 72)
```

### Customization

On first run the program creates the `nwggrid` folder in your .config directory. You'll find a sample template `bar.json`
and the `style.css` files inside.

Templates use json format. The default one defines an example Exit menu for sway window manager on Arch Linux:

```json
[
  {
    "name": "Lock screen",
    "exec": "swaylock -f -c 000000",
    "icon": "system-lock-screen"
  },
  {
    "name": "Logout",
    "exec": "swaymsg exit",
    "icon": "system-log-out"
  },
  {
    "name": "Reboot",
    "exec": "systemctl reboot",
    "icon": "system-reboot"
  },
  {
    "name": "Shutdown",
    "exec": "systemctl -i poweroff",
    "icon": "system-shutdown"
  }
]
```

You may use as many templates as you need, with the `-t` argument. All of them must be placed in the config directory.
You may use own icon files instead of icon names, like `/path/to/the/file/my_icon.svg`.

The style sheet makes the buttons look similar to `nwggrid`. You can customize them as well.

# nwgdmenu

This program provides 2 commands:

- `nwgdmenu` - displays newline-separated stdin input as a GTK menu
- `nwgdmenu_run` - creates a GTK menu out of commands found in $PATH

[![Swappshot-Mon-Mar-23-211702-2020.th.png](https://scrot.cloud/images/2020/03/23/Swappshot-Mon-Mar-23-211702-2020.th.png)](https://scrot.cloud/image/jfHK) [![Swappshot-Mon-Mar-23-211911-2020.th.png](https://scrot.cloud/images/2020/03/23/Swappshot-Mon-Mar-23-211911-2020.th.png)](https://scrot.cloud/image/j3MG) [![Swappshot-Mon-Mar-23-211736-2020.th.png](https://scrot.cloud/images/2020/03/23/Swappshot-Mon-Mar-23-211736-2020.th.png)](https://scrot.cloud/image/jvOi)

### Dependencies

- as above

### Installation

```
git clone https://github.com/nwg-piotr/nwg-launchers.git
cd nwg-launchers/dmenu
sudo make clean install
```
To uninstall:

```
sudo make uninstall
```

### Usage

```
$ nwgdmenu -h
GTK dynamic menu: nwgdmenu 0.0.1 (c) Piotr Miller 2020

nwgdmenu - displays newline-separated input stdin as a GTK menu
nwgdmenu_run - creates a GTK menu out of commands found in $PATH

Options [-h] [-ha <l>|<r>] [-va <t>|<b>] [-r <rows>] [-c <name>] [-o <opacity>]

Options:
-h            show this help message and exit
-ha <l>|<r>   horizontal alignment left/right (default: center)
-va <t>|<b>   vertical alignment top/bottom (default: middle)
-r <rows>     number of rows (default: 20)
-c <name>     css file name (default: style.css)
-o <opacity>  background opacity (0.0 - 1.0, default 0.3)
```

### Custom styling

On first run the program creates the `nwgdmenu` folder in your .config directory. You'll find the 
default `style.css` files inside. Use it to adjust styling and a vertical margin to the menu, if needed.

### i3 note

In case you use default window borders, an exclusion like this may be necessary:

```
for_window [title="~nwg"] border none
```

### Known issues

- `nwgdmenu -va <alignment> -ha <alignment>`, when started from terminal, behaves properly on sway only. On i3 and
Openbox the window appears in random places. However, when started from a key binding, it behaves as expected.
For now I have no idea what's the reason.
