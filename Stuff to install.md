## from pacman
~~~
sudo pacman -S kate steam gimp kdenlive qbittorrent virtualbox obs-studio pavucontrol vlc amd-ucode rofi ufw ttf-meslo-nerd ttf-ubuntu-font-family
discord obsidian neofetch eza spectacle neovim
~~~

## yay installation
~~~
sudo pacman -Syu
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
~~~

## from AUR
~~~
yay -S zoom
yay -S spotify
yay -S visual-studio-code-bin
yay -S postman-bin
yay -S brave-bin
~~~

## my folders to have
- ISOs
- Loi Liang Yang
- Wallpapers
- Dank net
- Clean coding and refactoring
- my neovim configuration

## Editing pacman
edit `/etc/pacman.conf`
- uncomment `#Color`
- add `ILoveCandy` below it
- enable `#ParallelDownloads` and set it to 5

## zsh & ohmyzsh
to be done after install because i forgot the process \

## Editing zsh
edit `.zshrc`
- theme = darkblood
- add alias towards the end of the file
  ~~~
  #My aliases
  alias ls='exa -al --color=always --group-directories-first'
  ~~~
- add `neofetch`(RIP) towards the end of the file

## nodejs and configuring nvm with zsh
~~~
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash
~~~

now to add nvm to my `.zshrc` file \
add this to the top of the file
~~~
# Initialize NVM
export NVM_DIR="$HOME/.nvm" 
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm 
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" # This loads nvm bash_completion
~~~

reload the terminal then
~~~
source ~/.zshrc
~~~

then install nodejs
~~~
nvm install [latest version number]
~~~

verify installation
~~~
node -v
npm -v
~~~

## Setting up the firewall and cache-cleaner
~~~
sudo ufw enable
sudo systemctl enable ufw.service

sudo systemctl enable paccache.timer
~~~

## Configuring grub
edit the `/etc/default/grub` \
change grub menu
~~~
GRUB_TIMEOUT_STYLE=hidden
~~~

configuring grub after change
~~~
sudo grub-mkconfig -o /boot/grub/grub.cfg
~~~


## Installing pipewire
installing pipewire and its dependencies, using pulseaudio plugin as well
~~~
sudo pacman -S pipewire pipewire-pulse pipewire-alsa pipewire-jack wireplumber
~~~

removing pulseaudio if already not removed
~~~
sudo pacman -Rns pulseaudio pulseaudio-bluetooth
~~~


enabling pipewire and wireplumber
~~~
systemctl --user enable pipewire pipewire-pulse
systemctl --user start pipewire pipewire-pulse

systemctl --user enable wireplumber.service
systemctl --user start wireplumber.service
~~~

verifying installation of audio drivers 
~~~
pactl info  //server name should be pulseaudio(on pipewire)

systemctl --user status pipewire pipewire-pulse  //should be active and running

systemctl --user status wireplumber  //should be active and running
~~~



