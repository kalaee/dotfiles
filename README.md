# Setup guide on minimal debian

This guide is partly inspired by [this blog](https://medium.com/hacker-toolbelt/i3wm-on-debian-10-buster-c302420853b1). I just collected some hints here for my future self.

## Setup the machine
First download the debian netinstall and setup the barebones version with all options de-selected.

When you can log in to the terminal add `contrib` and `non-free` after `main` in the file `/etc/apt/sources.list`. Now you run `sudo apt update && sudo apt upgrade`

Next I usually need to run this installation of nice/useful packages
```
sudo apt install xorg xinit i3 xterm firmware-iwlwifi dmenu build-essential git network-manager-gnome zathura firefox-esr chromium vim feh arandr alsa-utils xbacklight unzip zip imagemagick xserver-xorg-input-synaptics htop tmux ranger
```

Next you need to insert the present dotfiles into their respective places, the folders i3 and zathura belong inside `~/.config/`, and Xresources has the path `~/.Xresources`.

To find nice wallpapers that fit well with gruvbox check out [this collection](https://gitlab.com/exorcist365/wallpapers/-/tree/master/gruvbox) or perhaps even [the gruvbox factory](https://github.com/paulopacitti/gruvbox-factory)!
Inside the i3 config there is a feh command that fetches a random image from `~/Pictures/wallpapers/gruvbox/` when starting a session.

Now you are set with a nice gruvbox styled minimalist setup that can run on almost anything.

## Possible issue with backlight
If you have installed the package `xbacklight` and your machine cannot find the correct device for backlighting chances are that you need to identify that manually.
Check what folder you have in `/sys/class/backlight/`.
On my current Lenovo Thinkpad it is a folder named `intel_backlight/`.
In which case I create/edit the file `/etc/X11/xorg.conf` to read
```
Section "Device"
    Identifier  "Intel Graphics" 
    Driver      "intel"
    Option      "Backlight"  "intel_backlight"
EndSection
```
where `"intel_backlight"` is edited to be whatever the folder is named on your laptop.

## Setting up vim
