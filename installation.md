# Customized Fedora Installation Guide

This guide provides a list of commands to optimize the installation of Fedora for a faster setup.

## Table of Contents

- [Dependencies](#dependencies)
- [Additional Dependencies](#additional-dependencies)
- [Zsh Configuration](#zsh-configuration)
- [NPM without sudo Configuration](#npm-without-sudo-configuration)
- [Neovim Configuration](#neovim-configuration)
- [Appearance Configuration](#appearance-configuration)
- [Terminal Setup](#terminal-setup)
- [Librewolf Configuration](#librewolf-configuration)

## Installation

### Dependencies

- Install free, non-free and other necessary repositories:

```bash
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf config-manager --add-repo https://rpm.librewolf.net/librewolf-repo.repo
sudo dnf config-manager --add-repo https://cli.github.com/packages/rpm/gh-cli.repo
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
git clone https://github.com/Cryzen1/astronvim-config ~/.config/nvim/lua/user
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

- Install FiraCode Nerd Font:

```bash
https://github.com/ryanoasis/nerd-fonts/releases/latest/download/FiraCode.zip
```

- Extract FiraCode zip file:

```bash
tar -xvf FiraCode.zip ~/.local/share/fonts/FiraCode
```

### Terminal setup:

- Kitty installation:

```bash
curl -L https://sw.kovidgoyal.net/kitty/installer.sh | sh /dev/stdin
```

- Kitty configuration (located in "~/.config/kitty/kitty.conf" by default):

```bash
initial_window_width  1024
initial_window_height 640
font_family           FiraCode Nerd Font Mono Reg
font_size             12.0
remember_window_size  no
enable_audio_bell     no
cursor_shape          block
shell_integration     no-cursor
background            #222221
foreground            #e4e4e4
cursor                #ffffff
selection_background  #dedede
color0                #212121
color1                #b7141e
color2                #457b23
color3                #f5971d
color4                #134eb2
color5                #550087
color6                #0e707c
color7                #eeeeee
color8                #424242
color9                #e83a3f
color10               #7aba39
color11               #fee92e
color12               #53a4f3
color13               #a94dbb
color14               #26bad1
color15               #d8d8d8
selection_foreground  #222221
```

### Librewolf Configuration

- Copy librewolf.overrides.cfg into Librewolf's directory (located in "/usr/share/librewolf" by default):

```bash
sudo cp ./librewolf/librewolf.overrides.cfg /usr/share/librewolf/librewolf.overrides.cfg
```

- Copy policies.json into Librewolf's distribution directory (located in "/usr/share/librewolf" by default):

```bash
sudo cp ./librewolf/policies.json /usr/share/librewolf/distribution/policies.json
```
