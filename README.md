### Customização da distribuição Manjaro XFCE (https://manjaro.org) para se usar o Awesome Window Manager [AwesomeWM 4.3](https://awesomewm.org/)

### Customização Original design by PapyElGringo,  modified by Chris Titus. 

## Baseado no titus-awesome

Esta fork é apenas uma tentativa pessoal de melhorar meu modo de trabalho, aprender, compartilhar e não perder minhas ideias.

## Instalação

#### Manjaro XFCE

Todas minhas configuração foram sobre a base do Manjaro XFCE, com certeza deve funcionar em outras distros baseadas em Arch, mas alguns pacotes adicionais devem ser encessários.

# Instalar os pacotes:

Antes de instalar os pacotes deve-se instalar o yay. Para isso siga as instruções desse site: (https://www.linuxcapable.com/how-to-install-yay-aur-helper-on-manjaro-21-linux/)

###Instalar os pacotes necessários com esses comandos:

#### Com yay:
```
yay -S awesome rofi picom xclip ttf-roboto polkit-gnome materia-theme lxappearance flameshot network-manager-applet  qt5-styleplugins papirus-icon-theme i3lock i3lock-fancy-dualmonitor -y
```
#### Pacotes condizentes com os atalhos:
```
yay -S pnmixer discord thunderbird libreoffice nitrogen pamac-tray-icon-plasma nemo 
```
#### Apps utilitários e jogos:
```
yay -S obs-studio okular dropbox github-desktop-bin code scid
```

#### Apps para música:
```
yay -S musescore reaper cadence helm minuet jack2
```
#### Lista de programas para sistema

- [AwesomeWM](https://awesomewm.org/) as the window manager - universal package install: awesome
- [Roboto](https://fonts.google.com/specimen/Roboto) as the **font** - Debian: fonts-roboto Arch: ttf-roboto
- [Rofi](https://github.com/DaveDavenport/rofi) for the app launcher - universal install: rofi
- [picom](https://github.com/yshui/picom) for the compositor (blur and animations) universal install: picom - Debian users need PPA (`sudo add-apt-repository ppa:regolith-linux/unstable`) _Note: I recommend Compton for Debian Users and the Debian Branch_
- [i3lock](https://github.com/meskarune/i3lock-fancy) the lockscreen application universal install: i3lock-fancy
- [xclip](https://github.com/astrand/xclip) for copying screenshots to clipboard package: xclip
- [gnome-polkit] recommend using the gnome-polkit as it integrates nicely for elevating programs that need root access
- [Materia](https://github.com/nana-4/materia-theme) as GTK theme - Arch Install: materia-theme debian: materia-gtk-theme
- [Papirus Dark](https://github.com/PapirusDevelopmentTeam/papirus-icon-theme) as icon theme Universal Install: wget -qO- https://git.io/papirus-icon-theme-install | sh
- [lxappearance](https://sourceforge.net/projects/lxde/files/LXAppearance/) to set up the gtk and icon theme
- (Laptop) [xbacklight](https://www.x.org/archive/X11R7.5/doc/man/man1/xbacklight.1.html) for adjusting brightness on laptops (disabled by default)
- [flameshot](https://flameshot.org/) my personal screenshot utility of choice, can be replaced by whichever you want, just remember to edit the apps.lua file
- [pnmixer](https://github.com/nicklan/pnmixer) Audio Tray icon that is in debian repositories and is easily installed on arch through AUR.
- [network-manager-applet](https://gitlab.gnome.org/GNOME/network-manager-applet) nm-applet is a Network Manager Tray display from GNOME.
- 
### 2) Clonar os arquivos de configuração:

Arch-Based Installs
```
git clone https://github.com/Byronico-PRS/my_awesome1 ~/.config/awesome
```
### 3) Ligar configurações do Rofi com os arquivos de configuração já baixados

Configurações do menu Rofi

```
mkdir -p ~/.config/rofi
cp $HOME/.config/awesome/theme/config.rasi ~/.config/rofi/config.rasi
sed -i '/@import/c\@import "'$HOME'/.config/awesome/theme/sidebar.rasi"' ~/.config/rofi/config.rasi

```

### 4) Manter o mesmo tema para aplicações Qt/KDE e GTK, arruma os indicadores perdidos

First install  `qt5-styleplugins` (arch) and add this to the bottom of your `/etc/environment`

```bash
XDG_CURRENT_DESKTOP=Unity
QT_QPA_PLATFORMTHEME=gtk2
```

The first variable fixes most indicators (especially electron based ones!), the second tells Qt and KDE applications to use your gtk2 theme set through lxappearance.
### Ativar numlock no greeter

Com o pacote numlockx já instalado editar o o arquivo:

```
sudo nano /etc/lightdm/lightdm.conf
```
```
[Seat:*]
greeter-setup-script=/usr/bin/numlockx on
```
## Configuração de audio

Permitir ao Jack Realtime Scheduling

### 1 Editar arquivo de configuração:

```
sudo nano /etc/security/limits.conf
```
Este arquivo deve conter pelo menos essas duas linhas:
```
@audio   -  rtprio     95
@audio   -  memlock    unlimited
```
### 2 Criar o grupo de audio

Na instalação do seu sistema o grupo de audio pode já ter sido criado, caso isso não tenha ocorrido crie o grupo e adicione seu usuário:
```
groupadd audio
usermod -a -G audio ´usuario´
```
### 3 Reinicie o computador

Reinicie e as configurações de áudio já devem funcionar.
Verifique no Cadence no System Checks se o usuário está no grupo de áudio.

### 5) Read the documentation

The documentation live within the source code.

The project is split in functional directories and in each of them there is a readme where you can get additional information about the them.

* [Configuration](./configuration) is about all the **settings** available
* [Layout](./layout) hold the **disposition** of all the widgets
* [Module](./module) contain all the **features** available
* [Theme](./theme) hold all the **aesthetic** aspects
* [Widget](./widget) contain all the **widgets** available
