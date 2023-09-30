# Customized Fedora Installation Guide

This guide provides a list of commands to optimize the installation of Fedora for a faster setup.

## Table of Contents

- [Dependencies](#dependencies)
- [Additional Dependencies](#additional-dependencies)
- [Zsh Configuration](#zsh-configuration)
- [NPM without sudo Configuration](#npm-without-sudo-configuration)
- [Neovim Configuration](#neovim-configuration)
- [Appearance Configuration](#appearance-configuration)
- [XFCE4 Configuration](#xfce4-configuration)
- [Librewolf Configuration](#librewolf-configuration)

## Installation

### Dependencies

- Install free, non-free and other necessary repositories:

```bash
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf config-manager --add-repo https://rpm.librewolf.net/librewolf-repo.repo
sudo dnf config-manager --add-repo https://cli.github.com/packages/rpm/gh-cli.repo
```

- Uninstall unnecessary programs:

```bash
sudo dnf remove "*dnfdragora*" seahorse pragha gnome-abrt mailcap "*claws-mail*" "*geany*"
```

- Install necessary programs:

```bash
sudo dnf install gtk-murrine-engine sassc gnome-themes-extra cargo sqlite git zsh syncthing xclip gh neovim
```

### Additional Dependencies

- Install the additional dependencies for NVIDIA graphics drivers:

```bash
sudo dnf install akmod-nvidia
```

### ZSH Configuration

- Create the necessary directories for ZSH configuration:

```bash
mkdir -p ~/.zsh-essentials/{themes,plugins}
```

- Clone the Powerlevel10k theme repository for ZSH:

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/.zsh-essentials/themes/powerlevel10k
```

- Clone the ZSH Autocomplete plugin repository:

```bash
git clone --depth 1 -- https://github.com/marlonrichert/zsh-autocomplete.git ~/.zsh-essentials/plugins/zsh-autocomplete
```

- Clone the ZSH Syntax Highlighting plugin repository:

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.zsh-essentials/plugins/zsh-syntax-highlighting
```

- Source the Powerlevel10k theme and the ZSH plugins for syntax highlighting and autocompletion:

```bash
source "${HOME}/.zsh-essentials/themes/powerlevel10k/powerlevel10k.zsh-theme"
source "${HOME}/.zsh-essentials/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh"
source "${HOME}/.zsh-essentials/plugins/zsh-autocomplete/zsh-autocomplete.plugin.zsh"
```

### NPM without sudo Configuration

- Get the newest Node binaries from this URL: `https://nodejs.org/dist/latest/`

- Install Node binaries:

```bash
sudo cp -r {bin,share,lib,include} /usr/
```

- Create a directory for global NPM packages:

```bash
mkdir ~/.npm-packages
```

- Configure NPM to use the newly created directory as the prefix:

```bash
npm config set prefix "${HOME}/.npm-packages"
```

- Set the environment variable and add the NPM package directory to the system's `PATH`:

```bash
NPM_PACKAGES="${HOME}/.npm-packages"
export PATH="$PATH:$NPM_PACKAGES/bin"
```

### Neovim Configuration

- Clone the AstroNvim configuration repository for Neovim:

```bash
git clone https://github.com/AstroNvim/AstroNvim ~/.config/nvim
```

- Clone personal Neovim configuration repository to the appropriate location:

```bash
git clone https://github.com/<your_user>/<your_repository> ~/.config/nvim/lua/user
```

### Appearance Configuration

- Install Fluent GTK Theme:

```bash
git clone https://github.com/vinceliuice/Fluent-gtk-theme
cd ./Fluent-gtk-theme
./install.sh -t grey --tweaks solid round noborder
```

- Install Papirus Icon Theme:

```bash
wget -qO- https://git.io/papirus-icon-theme-install | DESTDIR="$HOME/.icons" sh
```

- Install Nerd Fonts:

```bash
https://github.com/ryanoasis/nerd-fonts/releases/latest
```

- Extract fonts:

```bash
tar -xvf <file_name> ~/.local/share/fonts/<file_name>
```

### XFCE4 Configuration

- Desktop setup:

```bash
xfconf-query -c xfce4-desktop -p /desktop-icons/file-icons/show-filesystem -n -t string -s false
xfconf-query -c xfce4-desktop -p /desktop-icons/file-icons/show-home -n -t string -s false
xfconf-query -c xfce4-desktop -p /desktop-icons/file-icons/show-removable -n -t string -s false
xfconf-query -c xfce4-desktop -p /desktop-icons/file-icons/show-trash -n -t string -s false
```

- Terminal setup:

```bash
xfconf-query -c xfce4-terminal -p /custom-command -n -t string -s /bin/zsh
xfconf-query -c xfce4-terminal -p /font-name -n -t string -s "FiraCode Nerd Font Mono 12"
xfconf-query -c xfce4-terminal -p /run-custom-command -n -t string -s true
```

- Panel setup:

```bash
xfconf-query -c xfce4-panel -p /panels/panel-2 -r -R
xfconf-query -c xfce4-panel -p /configver -n -t int -s 2
xfconf-query -c xfce4-panel -p /panels/dark-mode -n -t string -s true
xfconf-query -c xfce4-panel -p /panels/panel-1/icon-size -n -t int -s 22
xfconf-query -c xfce4-panel -p /panels/panel-1/length -n -t int -s 100
xfconf-query -c xfce4-panel -p /panels/panel-1/position-locked -n -t string -s true
xfconf-query -c xfce4-panel -p /panels/panel-1/size -n -t int -s 32
```

- Thunar setup:

```bash
xfconf-query -c thunar -p /default-view -n -t string -s ThunarDetailsView
xfconf-query -c thunar -p /last-details-view-column-widths -n -t string -s "50,126,124,50,50,50,50,50,530,226,111,263,50,152"
xfconf-query -c thunar -p /last-details-view-visible-columns -n -t string -s "THUNAR_COLUMN_DATE_ACCESSED,THUNAR_COLUMN_DATE_MODIFIED,THUNAR_COLUMN_NAME,THUNAR_COLUMN_SIZE,THUNAR_COLUMN_TYPE"
xfconf-query -c thunar -p /last-show-hidden -n -t string -s true
xfconf-query -c thunar -p /last-side-pane -n -t string -s ThunarShortcutsPane
xfconf-query -c thunar -p /last-toolbar-item-order -n -t string -s "0,1,2,3,4,5,6,7,8,9,12,13,14,15,11,10,16,17"
xfconf-query -c thunar -p /last-toolbar-visible-buttons -n -t string -s "0,1,1,1,0,0,0,0,0,0,0,0,1,0,1,1,1,1"
xfconf-query -c thunar -p /last-view -n -t string -s ThunarDetailsView
xfconf-query -c thunar -p /last-window-maximized -n -t string -s true
xfconf-query -c thunar -p /misc-date-custom-style -n -t string -s "%H:%M %d.%m.%Y"
xfconf-query -c thunar -p /misc-date-style -n -t string -s THUNAR_DATE_STYLE_CUSTOM
xfconf-query -c thunar -p /misc-directory-specific-settings -n -t string -s false
xfconf-query -c thunar -p /misc-full-path-in-tab-title -n -t string -s true
xfconf-query -c thunar -p /misc-single-click -n -t string -s false
```

- Appearance setup:

```bash
xfconf-query -c xsettings -p /Gtk/DecorationLayout -n -t string -s "close,maximize,minimize:menu"
xfconf-query -c xsettings -p /Net/IconThemeName -n -t string -s "Papirus-Dark"
xfconf-query -c xsettings -p /Net/ThemeName -n -t string -s "Fluent-round-grey-Dark"
xfconf-query -c xfwm4 -p /general/theme -n -t string -s "Fluent-round-grey-Dark"
xfconf-query -c xfwm4 -p /general/placement_ratio -n -t int -s 100
```

- Pointers setup:

```bash
xfconf-query -c pointers -p /Elan_Touchpad/Properties/libinput_Tapping_Enabled -n -t int -s 1
```

### Librewolf Configuration

- Find Librewolf's directory:

```bash
find / -name librewolf.cfg
```

- Copy librewolf.overrides.cfg into Librewolf's directory:

```bash
sudo cp ./librewolf/librewolf.overrides.cfg /usr/share/librewolf/librewolf.overrides.cfg
```

- Copy policies.json into Librewolf's distribution directory:

```bash
sudo cp ./librewolf/policies.json /usr/share/librewolf/distribution/policies.json
```
