<!-- TITLE: Shell Commands -->
<!-- SUBTITLE: Useful Shell Commands -->

# GNU/Linux
## General
| Command | Description |
|:--------|:------------|
| `xrandr --output HDMI-1 --same-as eDP-1` | Mirror screen of *eDP-1* to *HDMI-1*. |
| `xrandr --output HDMI-1 --left-of eDP-1` | Set screen *HDMI-1* virtually left of *eDP-1*. |
| `ip a` | List network interfaces. |
| `iwconfig` | List (wireless) network interfaces. |
| `ifconfig` | List network interfaces. |
| `ip link set wlan0 up/down` | Set interface *wlan0* up/down. |
| `systemctl restart networking.service` | Restart networking service. |
| <code>du -hs ./* &#124; sort -h</code> | Show disk usage sorted. |
| `rsync -av --delete /Source/ /Destination/` | Create a backup (see https://www.howtogeek.com/135533/how-to-use-rsync-to-backup-your-data-on-linux/). |
| `netctl restart profile-name` | Restart the specified profile. |

## Debian
| Command | Description |
|:--------|:------------|
| `apt-get clean` | Clean the apt cache. |

## Arch Linux
| Command | Description |
|:--------|:------------|
| `pacman -S package (e.g. archlinux-keyring)` | Update single package. |
| `pacman -Rdd package` | Force removing a package (ignoring dependencies). |

# Windows
| Command | Description |
|:--------|:------------|
| `robocopy source (e.g. L:\) destination (e.g. N:\) /mir /r:3 /w:5 /v /eta` | Create a backup. |