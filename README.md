### Customização da distribuição Manjaro XFCE (https://manjaro.org) para se usar o Awesome Window Manager [AwesomeWM 4.3](https://awesomewm.org/)

### Customização Original design by PapyElGringo,  modified by Chris Titus. 

## Baseado no titus-awesome

Esta fork é apenas uma tentativa pessoal de melhorar meu modo de trabalho, aprender, compartilhar e não perder minhas ideias.

## Instalação

#### Manjaro XFCE

Todas minhas configuração foram sobre a base do Manjaro XFCE, com certeza deve funcionar em outras distros baseadas em Arch, mas alguns pacotes adicionais devem ser encessários.

# Instalar os pacotes:

Antes de instalar os pacotes deve-se instalar o yay. Para isso siga as instruções desse site: (https://www.linuxcapable.com/how-to-install-yay-aur-helper-on-manjaro-21-linux/)

### Instalar os pacotes necessários com esses comandos:

#### Pacotes de tema:
```
yay -S awesome rofi picom xclip ttf-roboto polkit-gnome materia-theme lxappearance flameshot network-manager-applet qt5-styleplugins papirus-icon-theme i3lock i3lock-fancy-dualmonitors-git code pamac-tray-icon-plasma pnmixer -y
```
#### Pacotes condizentes com os atalhos:
```
yay -S discord thunderbird libreoffice nitrogen nemo brave-browser
```
#### Apps utilitários e jogos:
```
yay -S obs-studio okular dropbox github-desktop-bin scid dropbox
```

#### Apps para música:
```
yay -S musescore reaper cadence helm minuet jack2 pulseaudio-jack
```
#### Lista de programas para sistema e tema

- [AwesomeWM](https://awesomewm.org/) as the window manager - universal package install: awesome
- [Roboto](https://fonts.google.com/specimen/Roboto) as the **font** - Debian: fonts-roboto Arch: ttf-roboto
- [Rofi](https://github.com/DaveDavenport/rofi) for the app launcher - universal install: rofi
- [picom](https://github.com/yshui/picom) for the compositor (blur and animations) universal install: picom - Debian users need PPA (`sudo add-apt-repository ppa:regolith-linux/unstable`) _Note: I recommend Compton for Debian Users and the Debian Branch_
- [i3lock](https://github.com/meskarune/i3lock-fancy) the lockscreen application universal install: i3lock-fancy-dualmonitor
- [xclip](https://github.com/astrand/xclip) for copying screenshots to clipboard package: xclip
- [gnome-polkit] recommend using the gnome-polkit as it integrates nicely for elevating programs that need root access
- [Materia](https://github.com/nana-4/materia-theme) as GTK theme - Arch Install: materia-theme debian: materia-gtk-theme
- [Papirus Dark](https://github.com/PapirusDevelopmentTeam/papirus-icon-theme) as icon theme Universal Install: wget -qO- https://git.io/papirus-icon-theme-install | sh
- [lxappearance](https://sourceforge.net/projects/lxde/files/LXAppearance/) to set up the gtk and icon theme
- (Laptop) [xbacklight](https://www.x.org/archive/X11R7.5/doc/man/man1/xbacklight.1.html) for adjusting brightness on laptops (disabled by default)
- [flameshot](https://flameshot.org/) my personal screenshot utility of choice, can be replaced by whichever you want, just remember to edit the apps.lua file
- [pamac-tray-icon-plasma](https://gitlab.com/LordTermor/pamac-tray-icon-plasma) tray for pamac.
- [pnmixer](https://github.com/nicklan/pnmixer) Audio Tray icon that is in debian repositories and is easily installed on arch through AUR.
- [network-manager-applet](https://gitlab.gnome.org/GNOME/network-manager-applet) nm-applet is a Network Manager Tray display from GNOME.

#### Lista de programas condizentes com os atalhos
- [discord](https://github.com/discord) Discord A new way to chat with your communities and friends. Discord is the easiest way to communicate over voice, video, and text.
- [Thunderbird](https://www.thunderbird.net/en-US/get-involved/) E-mail Client
- [libreoffice](https://pt-br.libreoffice.org/) Suite Office
- [nitrogen](https://github.com/l3ib/nitrogen/) is a fast and lightweight (GTK2) desktop background browser and setter for X Window.
- [brave](https://brave.com/pt/) Brave is an open-source, privacy-focused web browser created by Brendan Eich (CEO) and Brian Bondy (CTO) through Brave Software.
- [nemo](https://github.com/linuxmint/nemo) Nemo is a free and open-source software and official file manager of the Cinnamon desktop environment
- [Code](https://code.visualstudio.com/) Visual Studio Code is a code editor redefined and optimized for building and debugging modern web and cloud applications. Visual Studio Code is free and available on your favorite platform - Linux, macOS, and Windows.

#### Lista de programas utilitários e jogos
- [Obs-Studio](https://obsproject.com/) Free and open source software for video recording and live streaming.
- [Okular](https://okular.kde.org/pt-br/) Multi-platform, fast and packed with features, Okular allows you to read PDF documents, comics and EPub books, browse images, visualize Markdown documents, and much more.
- [Dropbox](dropbox.com) Dropbox is a file hosting service operated by the American company Dropbox, Inc.
- [github](https://desktop.github.com/) Focus on what matters instead of fighting with Git. Whether you're new to Git or a seasoned user, GitHub Desktop simplifies your development workflow.
- [Scid](http://scid.sourceforge.net/) Study Chess Like You Mean It Manage databases with millions of games, analyze using UCI or Winboard engines, prepare for your next opponent, and much more. And it's Free and Open Source (GPL Licensed).

#### Lista de programas para música
musescore reaper cadence helm minuet jack2 pulseaudio-jack
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
