## from pacman
~~~
sudo pacman -S kate steam qbittorrent pavucontrol vlc amd-ucode rofi ufw ttf-meslo-nerd ttf-ubuntu-font-family discord obsidian fastfetch eza spectacle neovim ripgrep xclip kitty dolphin-plugins fzf thefuck zoxide wine proton-vpn-gtk-app reflector spotify-launcher dotnet-runtime dotnet-sdk lutris kwin rofi-wayland qt6-wayland xorg-xwayland
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
yay -S visual-studio-code-bin postman-bin brave-bin unityhub
~~~

## from flatpak(discover)
~~~
Photos
ProtonUp-Qt
Heroic
Zoom
~~~

## Editing pacman
edit `/etc/pacman.conf`
- uncomment `#Color`
- add `ILoveCandy` below it
- enable `#ParallelDownloads` and set it to 5

## zsh & ohmyzsh
~~~
sudo pacman -S zsh
~~~
then run zsh and choose option 1, which makes an empty `.zshrc` file

the do these to change shell to zsh
~~~
chsh -s $(which zsh)

cat /etc/passwd | grep $USER  // should show /usr/bin/zsh as abbas' shell

sudo reboot
~~~

to add oh-my-zsh
~~~
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" //see website first
~~~

## Editing zsh
edit `.zshrc`
theme = gentoo \

add the following to the end of your zsh to get zoxide,eza,thefuck,fzf
~~~
#Setting up eza(better ls)
alias ls="eza -al --color=always --group-directories-first --long --git --no-filesize --icons=always --no-time --no-user --no-permissions"

#Set up fzf key bindings and fuzzy completion
eval "$(fzf --zsh)"

#Setting up the fuck
eval "$(thefuck --alias)"

#Setting up zoxide(better cd)
eval "$(zoxide init zsh)"
alias cd="z"

fastfetch
~~~

## nodejs and configuring nvm with zsh
~~~
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash //see website first
~~~

now to add nvm to my `.zshrc` file \
add this to the top of the file (only if `nvm install [latest version]` doesnt work)
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


## Neovim setup
to do this only after git through ssh has been configured
~~~
git clone git@github.com:Abbas0024/my-neovim-config.git "${XDG_CONFIG_HOME:-$HOME/.config}"/nvim
~~~

and then initialise neovim for the first time
~~~
nvim
~~~

and then it will lazy-load and install all the plugins


## Mirror Ranking(in case of pacman errors)
~~~
sudo reflector --country 'India' --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
~~~

