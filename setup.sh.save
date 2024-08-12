#!/bin/bash

# pasta downloads/setup
mkdir -p $HOME/Downloads/setup-tmp
cd $HOME/Downloads/setup-tmp

# Atualizar repositorios
echo "Instalando e atualizando repositorios"
sudo apt update -y && sudo apt upgrade -y
sudo apt install curl wget git timeshift vim htop -y

# Instalando Brave
sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-release.list
sudo apt update -y
sudo apt install brave-browser -y

# driver adaptador wifi
git clone https://github.com/Mange/rtl8192eu-linux-driver
git clone https://github.com/luccasBB01/tl-wn821n
cd tl-wn821n
sudo cp tlwn821n.sh $HOME/Downloads/setup-tmp/rtl8192eu-linux-driver
cd $HOME/Downloads/setup-tmp/rtl8192eu-linux-driver
sudo ./tlwn821n.sh

# Instalando flatpak
sudo apt install flatpak -y
sudo apt install gnome-software-plugin-flatpak -y
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

# instalar docker
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
# Add Docker's official GPG key:
sudo apt-get update -y
sudo apt-get install ca-certificates curl -y
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update -y
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

# instalar hidamari
flatpak install flathub io.github.jeffshee.Hidamari

# papeis de parede hidamari
mkdir -p /$HOME/Documents/Wallpapers
cd /$HOME/Documents/Wallpapers

wallpapers=(
"https://mylivewallpapers.com/download/mobile-kyojuro-rengoku-forest-snow-live-wallpaper/?wpdmdl=58206&refresh=66b4063fe53981723074111"
"https://mylivewallpapers.com/download/4k-see-you-later-eren-live-wallpaper/?wpdmdl=52995&refresh=66b3f286ea1e91723069062"
"https://mylivewallpapers.com/download/3440x1440-kyojuro-rengoku-forest-snow-live-wallpaper/?wpdmdl=58205&refresh=66b4063fca0861723074111"
"https://mylivewallpapers.com/download/qhd-akane-sgail-toriel-live-wallpaper/?wpdmdl=57850&refresh=66b3ed3cbece81723067708"
"https://mylivewallpapers.com/download/4k-sekiro-mortal-blade-live-wallpaper/?wpdmdl=57787&refresh=66b4076c4c7f21723074412"
"https://mylivewallpapers.com/download/4k-eren-yeager-and-titan-live-wallpaper/?wpdmdl=54160&refresh=66b3e39354c4b1723065235"
"https://mylivewallpapers.com/download/ambush-aot-live-wallpaper/?wpdmdl=34622&refresh=66b40922c8f741723074850"
)

for wallpaper in "${wallpapers[@]}"; do
	echo "Baixando $wallpaper"
	wget ¨wget -q "$wallpaper"
done


flatpak run io.github.jeffshee.Hidamari

# baixar vscode
sudo apt-get install wget gpg -y
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" |sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null
rm -f packages.microsoft.gpg
sudo apt install apt-transport-https -y
sudo apt update -y
sudo apt install code -y # or code-insiders


# reiniciar após configurações
sudo systemctl reboot
