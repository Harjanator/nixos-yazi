[![NixOS 26.05+](https://img.shields.io/badge/NixOS-26.05%2B-a6e3a1?labelColor=45475a)](https://nixos.org/)
[![License MIT](https://img.shields.io/badge/License-MIT-cba6f7.svg?labelColor=45475a)](LICENSE.md)
[![Portal](https://img.shields.io/badge/Portal-typovrak.tv%2Fnixos-eba0ac?labelColor=45475a)](https://typovrak.tv/nixos)
[![Discord join us](https://img.shields.io/badge/Discord-Join%20us-74c7ec?labelColor=45475a&logo=discord&logoColor=white)](https://typovrak.tv/discord)

<div>
  <a href="https://visitorbadge.io/status?path=https%3A%2F%2Fgithub.com%2Ftypovrak%2Fnixos-yazi"><img src="https://api.visitorbadge.io/api/visitors?path=https%3A%2F%2Fgithub.com%2Ftypovrak%2Fnixos-yazi&label=GET%20https%3A%2F%2Fgithub.com%2Ftypovrak%2Fnixos-yazi&labelColor=%23a6e3a1&countColor=%231e1e2e" /></a>
</div>

# 📂 NixOS Yazi

> 🔧 NixOS module for automated Yazi document viewer setup: configuration, themes and color schemes.

## 🧩 Part of the Typovrak NixOS ecosystem

This module is part of ```Typovrak NixOS```, a fully modular and declarative operating system configuration built entirely with :

- 🧱 **30+ standalone modules :** Each managing a specific tool, feature or aesthetic like ```zsh```, ```i3```, ```lighdm```, ```polybar```, ```gtk``` and more.
- 🎨 **Catppuccin Mocha :** The default theme across terminal, GUI, and login interfaces.
- 🛡️ **100% FOSS compliant :** No proprietary software included unless explicitly chosen.
- 🧑‍💻 **Built for developers :** Optimized for speed, keyboard-centric workflows and expressive CLI tooling.

*Explore the full system : 👉 [github.com/typovrak/nixos](https://github.com/typovrak/nixos)*

> [!CAUTION]
> This module is opinionated, it may **override**, **replace**, or **remove** files and settings **without** prompt. To avoid unexpected changes, **back up** your existing files or **fork** this module to take full control. **Follow this documentation** to avoid any of this problem.

## 📦 Features

- 🔒 **Secure config directory :** Creates and protects ```~/.config/yazi``` with correct ownership and permissions.
- 🎨 **Theme & color schemes :** Installs ```~/.config/yazi/yazi.toml```, ```~/.config/yazi/theme.toml```, and ```~/.config/yazi/Catppuccin-mocha.tmTheme``` into the user’s config.
- 🔄 **Idempotent :** Cleans and recreates config on each rebuild for consistent setup.
- ⚙️ **Zero-friction setup**: Works out-of-the-box with minimal options.
- 📦 **Dependency handling :** Ensures ```yazi``` is added to ```environment.systemPackages```.
- 💾 **Backups**: Backup commands for existing configs are detailed in the docs.

## 📂 Repository structure

```bash
❯ tree -a -I ".git*"
.
├── Catppuccin-mocha.tmTheme #
├── configuration.nix        # module configuration
├── LICENSE.md               # MIT license
├── README.md                # this documentation
├── theme.toml               #
└── yazi.toml                #

1 directory, 6 files
```

## ⚙️ Prerequisites

### 1. NixOS version
Requires NixOS 24.11 or newer.

### 2. User validation
the target user must be defined in ```config.username```. See [typovrak main nixos configuration](https://github.com/typovrak/nixos) for more details.

### 3. Backup
Before proceeding, back up existing configuration if needed
```bash
cp ~/.config/yazi{,.bak}
```

## ⬇️ Installation

### 🚀 Method 1 : Out-of-the-box

Fetch the module directly in your [main nixos configuration](https://github.com/typovrak/nixos) at ```/etc/nixos/configuration.nix``` using fetchGit
```nix
# /etc/nixos/configuration.nix

let
  nixos-yazi = fetchGit {
    url = "https://github.com/typovrak/nixos-yazi.git";
    ref = "main";
    rev = "6d5c026706aa35d57c1ba50abc83ee05525ab816"; # update to the desired commit
  };
in
{
  imports = [
    /etc/nixos/hardware-configuration.nix # system hardware settings
    /etc/nixos/variables.nix # defines config.username and other variables, see https://github.com/typovrak/nixos for more details
    (import "${nixos-yazi}/configuration.nix")
  ];
}
```

Once imported, rebuild your system to apply changes
```bash
sudo nixos-rebuild switch
```

### 🍴 Method 2 : Fork

Want to **personalize** this module ?

Fork it and add this custom module in your [main nixos configuration](https://github.com/typovrak/nixos) at ```/etc/nixos/configuration.nix``` using fetchGit
```nix
let
  nixos-yazi = fetchGit {
    url = "https://github.com/<YOUR_USERNAME>/nixos-yazi.git";
    ref = "main";
    rev = "<COMMIT>"; # see below
  };
in {
  imports = [
    /etc/nixos/hardware-configuration.nix # system hardware settings
    /etc/nixos/variables.nix # defines config.username and other variables, see https://github.com/typovrak/nixos for more details
    (import "${nixos-yazi}/configuration.nix")
  ];
}
```

Get the latest commit hash by executing
```bash
git clone https://github.com/<YOUR_USERNAME>/nixos-yazi.git &&
cd nixos-yazi &&
git log -1 --pretty=format:"%H"
```

## 🎬 Usage

Open directories with the ```yazi``` command in your terminal, with ```xdg-open .``` if yazi is your default file explorer or with the dmenu in i3.

## 📚 Learn more

- 🧠 [Yazi GitHub repository](https://github.com/sxyazi/yazi) : Official source code and project documentation.
- 🎨 [Catppuccin for Yazi](https://github.com/catppuccin/yazi) : Mocha theme and integration with the Catppuccin ecosystem.
- 📁 [```mkdir -p ~/.config/yazi```](https://man7.org/linux/man-pages/man1/mkdir.1.html) : Ensure the config directory exists before applying changes.

## 🌐 Discover my NixOS system portal

Dive into [typovrak.tv/nixos](https://typovrak.tv/nixos) Catppuccin mocha green themed **gateway** to my GitHub and NixOS setup.

Browse **every module**, example and config in a sleek with an interactive interface that feels just like your desktop.

## ❤️ Support

If this module saved you time, please ⭐️ the repo and share feedback.

## 💬 Join the Typovrak community on Discord 🇫🇷

If you've ever ```rm -rf```ed your config by mistake or rebuilt for the 42nd time because a semicolon was missing…

You're not alone, **Welcome home !**

🎯 [Join us on Discord »](https://typovrak.tv/discord)

🧭 What you’ll find is :

- ```💻 #nixos-setup``` - get help with modules, rebuilds and configs.
- ```🌐 #web-dev``` - talk JS, TypeScript, React, Node and more.
- ```🧠 #open-source``` - share your repos, contribute to others and discuss FOSS culture.
- ```⌨️ #typing``` - layouts, mechanical keyboards and speed goals.
- ```🎨 #ricing``` - dotfiles, theming tips and desktop screenshots.

*Everyone's welcome no matter how many times you've broken your system ~~(except for Windows users)~~ 😄*

---

<p align="center"><i>Made with 💜 by <a href="https://typovrak.tv">typovrak</a></i></p>
