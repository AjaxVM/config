# Tweaks I made to my antergos/xfce4 installation to get things working properly

## Non-Visual Tweaks

* make super/windows key open whisker menu
 * `xmodmap -e "keycode 115 = Menu" &`
* get optimus working (nvidia+intel graphics)
 * uninstall nvidia/nouveau
 * install `optimus-manager-git` and `optimus-manager-qt-git` (AUR)
 * `sudo systemctl enable optimus-manager.service`
 * `sudo systemctl start optimus-manager.service`
 * `optimus-manager --set-startup intel`
 * add optimus-manager-qt (Optimus Manager UI) to xfce startup (autostart)
* disable hibernate (I use suspend and didn't want to add swap for hibernate)
 * `xfconf-query -c xfce4-session -np '/shutdown/ShowHibernate' -t 'bool' -s 'false'`
 * disable Hibernate (replace with suspend for sleep) in Power Manager
* Install Razer Drivers/RGB controls
 * install `openrazer-meta` (AUR)
 * install `dkms` (AUR) - if not already
 * `sudo dkms install razer_chroma_driver/1.0.0
  * I installed `linux-headers` which is apparently sometimes needed by dkms, not sure if needed or not here
 * install `razercommander-git` (AUR)
* Ensure bluetooth is disabled (didn't install drivers so think that is ok with installer)
* I played around a bit with `pstate-frequency` and `intel_pstate` to try to help battery life, didn't seem to have much effect
* Change the lightdm greeter (it doesn't support tap to click and not a fan in general of webkit2)
 * install `slick-greeter`
 * edit `/etc/lightdm/lightdm.conf` (to enable slick-greeter)
 * make sure background/wallpaper is accessible (I put in `/opt`)
* Add gesture support (just care about two-finger right-click myself)
 * install `libinput-gestures` and `gestures` (both AUR)
* Enable trim (weekly cron)
* Fix slow shutdown
 * Ended up being an issue with LVM
 * [systemd github issue comment](https://github.com/systemd/systemd/issues/11821#issuecomment-477545885) presents the proper fix, create that dir/file and add the Unit check
* Tweak terminal hotkeys (no physical home/page down/etc. keys)
 * enable gtk accel (Appearance->Settings->"Enable editable accelerators")
 * `mkdir -p ~/.config/xfce4/terminal`
 * edit `~/.config/xfce4/terminal/accels.scm`
  * **next tab**: ctrl (primary) + right
  * **last tab**: ctrl + left
  * **new tab**: ctrl + t
  * **close tab**: ctrl + w
* Tweak workspace controls
 * open "Window Manager"->Keyboard
 * switch workspace: ctrl + alt + arrow
 * move current window: ctrl + super + alt + arrow
 * tile window to edge: ctrl + fn + arrow (does home/pageup/etc with fn)
 * tile window to corner: ctrl + super + arrow
 * maximize window: ctrl + super + return
* Open Task Manager
 * open Keyboard->"Application Shortcuts"
 * set `xfce4-taskmanager` to use shift + ctrl + escape

## Theming/Visual Tweaks

* Theming
 * **icon pack**: papyrus-blue
 * **theme**: flat-plat-blue (dark-compact)
  * weird bug with google docs title being dark grey with this one :(
 * **cursor**: DMZ (XFCE White)
 * **system font**: Lato (10)
 * **mono font**: DejaVu Sans Mono Book (10)
* Panel setup
 * install `xfce4-goodies`
  * go back and remove ones you don't want - was like 20 for me (like orage clock)
  * https://www.archlinux.org/groups/x86_64/xfce4-goodies/
 * use `DateTime` plugin for clock
  *time then date, Lato (12) font
 * workspaces: 2x2
 * install `dockbarx` and `xfce4-dockbarx-plugin`
  * **theme**: Sunny Colors
  * **window list style**: Magic Transparency
  * **needs attn**: blink
 * remove original window buttons/etc.
 * add second panel
  * bottom-right
  * not fill
  * add `Battery Monitor` item
   * display label
   * display bar
   * display percentage
   * display time
   * display percentage in tooltip
   * displat time remaining in tooltip
  * add `Sensor plugin`
   * show gpu (nouveau, have to rename proper sensor)
   * show cpu (coretemp-0, have to rename)
  * intelligent hide
 * panel color: #1F4366
 * panel alpha: 80
 * row size: 40
* remove roll up button (I just like standard 3 buttons)
 * in Settings->Window Manager, just remove the item from button layout
