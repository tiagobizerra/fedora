# Minisforum UM890 Pro — Workstation Configuration Log

Comprehensive post-installation layout tracking the setup parameters, development engines, and custom localization matrices implemented on Fedora 44 GNOME.

---

## Machine Specifications
- **Hardware:** Minisforum UM890 Pro (AMD Ryzen 9 8945HS, 32 GB DDR5, 512 GB SSD)
- **Operating System:** Fedora 44 Workstation
- **Display Server:** Wayland
- **Desktop Environment:** GNOME 47+

---

## Completed Implementations

### Steps 1–3: Installation Base Layer
- Clean installation of Fedora Workstation executed.
- Core Windows partitions completely wiped.
- Secure Boot explicitly disabled in the system BIOS to prevent kernel module loading conflicts.

---

### Step 4: Peripherals Integration
- **Apple USB Classic Keyboard:** Native plug-and-play architecture functional.
- **Apple Magic Mouse 2:** Paired over native GNOME Bluetooth stack.
- **Natural Scrolling Configuration:** Enabled to mirror macOS axis metrics:
  ```bash
  gsettings set org.gnome.desktop.peripherals.mouse natural-scroll true
  ```
- **Middle-Click Paste Suppression:** Disabled mouse middle-click paste natively to preserve developer copy buffers:
  ```bash
  gsettings set org.gnome.desktop.interface gtk-enable-primary-paste false
  ```
- **Persistent Autostart Enforcement:** Handled via custom desktop initialization profile stored at `~/.config/autostart/disable-middle-paste.desktop`:
  ```ini
  [Desktop Entry]
  Type=Application
  Name=Disable middle click paste
  Exec=gsettings set org.gnome.desktop.interface gtk-enable-primary-paste false
  X-GNOME-Autostart-enabled=true
  ```

---

### Step 4b: Trilingual Keyboard Layout Engine & Text Matrix
- **Hardware Target Profile:** Keychron K2 V3 (75% Compact ANSI Layout) physical toggle switch locked permanently to **Mac Mode** to maintain optimal spacebar-modifier gaps.
- **System Interface Language:** Set to `English (United States)`.
- **Keyboard Layout Mapping Selection:** Configured in GNOME System Settings to use **English (US, intl., with dead keys)**.
- **Wayland IBus Framework Enforcement:** Forced GNOME's text translation subsystem under Wayland to prioritize local user character tables:
  ```bash
  gsettings set org.gnome.desktop.interface gtk-im-module "xim"
  ```
- **The Trilingual Matrix Layer (~/.XCompose):** Resolves structural language syntax collisions between English, Brazilian Portuguese, and Spanish. Suppresses unwanted Eastern-European consonant combinations (like `ś`, `ć`, `ǘ`, `ẃ`) while preserving native vowels (`á`, `ã`, `â`, `à`) and symbols (`ç`, `ñ`). Standard English contractions like `let's` print instantly on a single stroke.

---

### Step 5: Drop-Down Terminal Utility (ddterm)
- **Strategy Selection:** Standard dropdown terminal tools (like Guake or Yakuake) cause execution conflicts on Python 3.14 or drag in bloated desktop framework stacks. To maintain a clean Wayland shell session natively under GNOME, `ddterm` was installed.
- **Installation via CLI:**
  ```bash
  sudo dnf install gnome-shell-extension-ddterm -y
  ```
- **Activation:** The extension was toggled ON inside the `gnome-extensions-app` manager.
- **Shortcut Configuration:** The global drop-down activate-window binding was locked to the user choice: **`Alt + X`**.

---

### Step 6: Zsh Profile & Oh My Zsh Framework
- **Shell Target Installation:** 
  ```bash
  sudo dnf install zsh -y
  chsh -s \$(which zsh)
  ```
- **Automated Oh My Zsh Framework Installer:**
  ```bash
  sh -c "\$(curl -fsSL https://githubusercontent.com)"
  ```
- **Plugin Extensions Cloned Natively Into User Space:**
  ```bash
  git clone https://github.com ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions
  git clone https://github.com ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting
  ```

---

### Step 7: Legacy Apple Time Capsule Integration
- **Infrastructure Connection Track:** `smb://<TIME_CAPSULE_IP>/<SHARE_NAME>`
- Connected cleanly using Fedora's native user virtualization backend layer (`gio` mount protocols) within Nautilus.
- SMBv1 legacy protocol switches verified to handle authorization handshakes with legacy hardware filesystems securely.
- Mount structures safely managed in unprivileged user space.

---
---

### Step 8: GitHub Profiles & Cryptographic Key Architectures
- **Secure SSH Key Generation:** Created over the fast Ed25519 elliptic curve scheme:
  ```bash
  ssh-keygen -t ed25519 -C "your-email@example.com"
  ```
- **GPG Commit Verification Key Generation:** Built a 4096-bit RSA signing key:
  ```bash
  gpg --full-generate-key
  ```
- **Automatic Local Git Commit Signing Configuration:**
  ```bash
  git config --global commit.gpgsign true
  git config --global user.signingkey <GPG_KEY_ID>
  ```
- **TTY Terminal Session Binding:** Linked natively inside your shell setup file:
  ```bash
  export GPG_TTY=\$(tty)
  ```

---

### Step 9: Cursor Editor Workspace
- **Stored Binary Location:** Managed inside your user path layout: `~/.local/bin/cursor.AppImage`
- **Custom Application Launcher Profile:** Generated at `~/.local/share/applications/cursor.desktop`:
  ```ini
  [Desktop Entry]
  Name=Cursor
  Exec=/home/tiagolima/.local/bin/cursor.AppImage --no-sandbox %F
  Icon=/home/tiagolima/.local/share/icons/cursor.svg
  Type=Application
  Categories=Development;TextEditor;
  Terminal=false
  MimeType=text/plain;
  StartupWMClass=Cursor
  ```
- **Vector Branding Asset:** Crisp, scalable SVG file pulled down natively directly from `https://cursor.com`.

---

### Step 10: Multi-Engine Browser Suites
- **Mozilla Firefox:** Open-source baseline track active.
- **Google Chrome:** Standard production stable distribution repository.
- **Brave Browser:** Chromium utility running with privacy shields active.

---

### Step 11: 1Password Integration
- **Production Repository Channel Enforcement:** 
  ```bash
  sudo rpm --import https://1password.com
  sudo sh -c 'echo -e "[1password]\nname=1Password Stable Channel\nbaseurl=https://1password.com\$basearch\nenabled=1\ngpgcheck=1\nrepo_gpgcheck=1\ngpgkey=\"https://1password.com\"" > /etc/yum.repos.d/1password.repo'
  sudo dnf install 1password 1password-cli -y
  ```
- **Biometric Handshakes:** Tuned application configurations to securely pass unlock authentication tokens natively into the GNOME environment via key system policies.

---

### Step 12: Python Isolation Layer (pyenv)
- **System Compilation Dependencies:** Required for flawless background source builds:
  ```bash
  sudo dnf install bzip2-devel readline-devel sqlite-devel openssl-devel xz-devel zlib-devel libffi-devel tcl-devel tk-devel -y
  ```
- **Automated Installer Core:** Triggered over web source tracks:
  ```bash
  curl https://pyenv.run | bash
  ```
- **Zsh Initialization Profile Injection:** Mapped to handle paths and virtualization hooks:
  ```bash
  export PYENV_ROOT="\$HOME/.pyenv"
  [[ -d \$PYENV_ROOT/bin ]] && export PATH="\(PYENV_ROOT/bin:\)PATH"
  eval "\$(pyenv init -)"
  eval "\$(pyenv virtualenv-init -)"
  ```
- **Default Workspace Runtime:** Set to stable development rails: `pyenv global 3.12`

---

### Step 13: Docker Virtualization Stack
- Conflicting native layout engine options (like `podman`) dropped to establish absolute workspace integrity.
- **Official Production Engine Script Deployment:** Upstream daemon tools installed directly to avoid local repo blocks:
  ```bash
  curl -fsSL https://docker.com -o get-docker.sh
  sudo sh get-docker.sh
  sudo systemctl enable --now docker
  ```
- **Unprivileged Non-Root Execution Permissions:** Userspace linked to container engine parameters group:
  ```bash
  sudo usermod -aG docker \$USER
  ```

---

### Step 14: GNOME System Tweaks & Extension Architectures
- **Universal Flatpak Hub Initialization:**
  ```bash
  flatpak remote-add --if-not-exists flathub https://flathub.org
  ```
- **Extensions Tree Ecosystem:** Dash to Dock, AppIndicator Support, Clipboard Indicator, Vitals, Hot Corners Extended.

---

### Step 15: Spotify Client
- **Sandbox Application Deployment:** Loaded cleanly through flatpak platform parameters:
  ```bash
  flatpak install flathub com.spotify.Client -y
  ```

---

### Step 16: Claude AI Engineering Workspace
- **Node.js Environment Prerequisite:** Runtime stack deployed to compile the CLI utility:
  ```bash
  sudo dnf install nodejs npm -y
  ```
- **Claude Code Installation:** Deployed globally to active execution paths:
  ```bash
  sudo npm install -g @anthropic-ai/claude-code
  ```
- **Claude Desktop Web-Container App:** Standard application launcher constructed to lock Claude into a lightweight Chrome application viewport window:
  ```ini
  [Desktop Entry]
  Name=Claude
  Exec=google-chrome --app=https://claude.ai
  Icon=google-chrome
  Type=Application
  Categories=Development;WebBrowser;
  Terminal=false
  StartupWMClass=claude.ai
  ```

---

## Technical Decision Registry
- **Guake / Yakuake / Kitty Dropdown Rejection:** Blocked due to installation failures on modern Python 3.14 layers or excessive dependency weight. Completely replaced by the streamlined GNOME extension `ddterm`.
- **Keyboard Global Shortcut Layouts (Cmd+C / Cmd+V Remapping):** Abandoned system-wide software translation rules to avoid broken navigation nodes inside desktop window layers. Custom key combinations map special alphabetic variations and accents cleanly through local user tables (`~/.XCompose`), while baseline desktop actions remain on standard, stable Linux patterns (`Ctrl+C` / `Ctrl+V`).
- **Apple Time Capsule Persistent Automation:** Systemd background unit configurations and native GNOME graphical autostart chains were discarded. Legacy SMBv1 requirements and interactive keyring credential requests under Wayland cause background freezes. The share was transitioned to a clean, custom manual script mapping track (`time-capsule`) located in `~/.local/bin/`.

---

## Remaining Pending Tasks

- [ ] **Step 7c:** Troubleshoot and fix Apple Time Capsule network mounting to make it initialize reliably during the boot sequence without human interaction.
- [ ] **Step 17:** Migration of local data blocks over network from old white MacBook.
- [ ] **Step 7b:** Configuring automated background data backup sync using Deja Dup tracking target Time Capsule directories.

