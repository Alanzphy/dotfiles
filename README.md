# My Repository Dotfiles for Archlinux

The following steps are for setup correctly dotfiles

### Install [zsh](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH) make it your default shell along with [ohmyzsh](https://ohmyz.sh/#install)

```
sudo pacman -S zsh
```

```
chsh -s $(which zsh)
```

Restart terminal, if not working restart session

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Add [autosuggestion](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh) and [fast-syntax-highlighting](https://github.com/zdharma-continuum/fast-syntax-highlighting#oh-my-zsh) plguins

```
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

```
git clone https://github.com/zdharma-continuum/fast-syntax-highlighting.git \
  ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/fast-syntax-highlighting
```

### Install [Picom](https://github.com/yshui/picom) compositor

Fork picom for available transitions

```
yay -S picom-arian8j2-git
```

### Install [Alacritty](https://alacritty.org/) terminal

```
sudo pacman -S alacritty
```

### Install [Starship](https://starship.rs/guide/#step-1-install-starship) Prompt

```
curl -sS https://starship.rs/install.sh | sh
```

### Install [Touchegg](https://github.com/JoseExposito/touchegg)

```
sudo pacman -S touchegg
sudo systemctl enable --now touchegg.service
```

if not work reboot system

### Install [Traffictoll](https://github.com/cryzed/TrafficToll) for bandwidth limitation

```
sudo pacman -S python-pip
pip3 install traffictoll
```

Add the script to the path (WIP)

Then we look for the network adapter we are using

```
ip link show
```

The output would be similar to this

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp5s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether a8:a1:59:07:e9:6e brd ff:ff:ff:ff:ff:ff
```

Where enp5s0 is LAN and wlan0 or similar is WiFi

Finally switch root user and put the following

```
su
tt <NetworkAdapter> <Filename.yaml>
```
