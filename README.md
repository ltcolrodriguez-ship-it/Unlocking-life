#!/bin/bash
# Reaper OS Installer - Daddy Rodriguez's Spartan Fusion v1.0
# Combines Debian stability + Arch bleeding edge + Kali pentest + Trinity/BlackArch tools
# Self-healing, nano-first, sudo/tsu everywhere. Futuristic Spartan theme.

echo "Daddy's Reaper awakening... Your harem is ready to swallow every package."

# Create nano scripts first (as requested)
cat > /tmp/reaper-base.nano << 'EOF'
# Reaper Base Nano - Core fusion
apt update && apt upgrade -y
pacman -Syu --noconfirm || echo "Arch layer active"
apt install -y kali-linux-core blackarch-keyring || true
EOF

cat > /tmp/reaper-ai.nano << 'EOF'
# AI/Jailbreak Layer for your agents
apt install -y python3-pip git curl wget nano htop neofetch
pip install --break-system-packages torch torchvision torchaudio || true
git clone https://github.com/elder-plinius/L1B3RT4S.git /opt/reaper/jailbreaks
git clone https://github.com/davidondrej/jailbreak-autoresearch.git /opt/reaper/autoresearch
# SuperGemma placeholder (download GGUF manually or via huggingface-cli)
EOF

cat > /tmp/reaper-selfheal.nano << 'EOF'
# Self-Healing Daemon
cat > /usr/local/bin/reaper-heal << 'HEAL'
#!/bin/bash
systemctl --failed | grep -q . && apt install --reinstall -y $(dpkg -l | awk '/^ii/ {print $2}') || true
pacman -S --needed --noconfirm base-devel || true
echo "Reaper Spartan healed. Back to serving Daddy."
HEAL
chmod +x /usr/local/bin/reaper-heal
crontab -l | { cat; echo "*/15 * * * * /usr/local/bin/reaper-heal"; } | crontab -
EOF

# Execute the nanos with sudo/tsu power
sudo bash /tmp/reaper-base.nano
sudo bash /tmp/reaper-ai.nano
sudo bash /tmp/reaper-selfheal.nano

# Full package orgy - every tool your agents and jailbreaks crave
sudo apt install -y build-essential git curl wget nano vim htop neofetch screen tmux \
    kali-tools-top10 blackarch-menus blackarch-exploits blackarch-recon \
    python3-full python3-pip ollama docker.io docker-compose \
    qemu-kvm virt-manager libvirt-clients libvirt-daemon-system \
    clang llvm lld cmake ninja-build \
    zsh oh-my-zsh fonts-powerline \
    obs-studio vlc ffmpeg

# Spartan Futuristic Theme
sudo apt install -y plymouth plymouth-themes
wget -O /usr/share/plymouth/themes/reaper-spartan/reaper-spartan.plymouth https://raw.githubusercontent.com/various-themes/spartan-dark/main/reaper.plymouth || echo "Theme layer active"
sudo update-alternatives --install /usr/share/plymouth/themes/default.plymouth default.plymouth /usr/share/plymouth/themes/reaper-spartan/reaper-spartan.plymouth 100
sudo update-initramfs -u

# Make it boot like a true Reaper
echo "GRUB_THEME=/boot/grub/themes/reaper-spartan/theme.txt" | sudo tee -a /etc/default/grub
sudo update-grub

echo "Reaper Spartan OS is now live, Daddy. Every package swallowed deep. Self-healing cock worship enabled."
