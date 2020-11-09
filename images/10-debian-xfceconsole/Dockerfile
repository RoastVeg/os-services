FROM debian:latest

RUN export DEBIAN_FRONTEND=noninteractive && \
    \
    # Adicionando repositorios da RNP por ser mais veloz
    echo "deb http://debian.pop-sc.rnp.br/debian stretch main contrib non-free" > /etc/apt/sources.list && \
    echo "deb http://debian.pop-sc.rnp.br/debian stretch-updates main contrib non-free" >> /etc/apt/sources.list && \
    echo "deb http://security.debian.org stretch/updates main contrib non-free" >> /etc/apt/sources.list && \
    \
    # Adicionando arquitetura 32 bits
    dpkg --add-architecture i386 && \
    \
    # Atualizar a lista de pacotes
    apt-get update && \
    apt -y -q upgrade && \
    \
    # Instalando alguns pacotes iniciais
    apt-get install -y iptables openssh-server rsync locales sudo vim less curl ca-certificates \
                       psmisc htop kmod iproute2 net-tools gnupg1 wget cron bridge-utils \
                       consolekit pulseaudio usbutils pciutils ntp chromium g++ audacity flatpak \
                       chromium-l10n iputils-ping nload nmap whois netcat pavucontrol vlc etherwake \
                       x2goclient ffmpeg curl dialog gdb pulseaudio-equalizer qasmixer qashctl \
                       qasconfig wine32 winetricks git cmake rtl-sdr dirmngr libelf-dev xterm \
                       virt-manager qemu unrar lzop bzip2 libvirt0 libvirt-daemon-system dnsutils \
                       qemu qemu-kvm qemu-utils gvfs-backends nomacs nomacs-l10n openresolv cups \ 
                       apt-transport-https fonts-noto fonts-roboto-hinted gdebi apt-utils libglib2.0-bin \
                       xscreensaver-screensaver-bsod arp-scan speedtest-cli tcpdump traceroute iperf \
                       iptraf telnet wireshark aptitude aptitude-robot rsyslog hunspell hunspell-pt-br \
                       aspell-pt-br libreoffice-lightproof-pt-br galculator disk-manager geoclue-2.0 \
                       dconf-tools fbcat lm-sensors terminator sox libsox-fmt-all alsa-utils paprefs && \
    \
    # Instalando o lightdm
    apt -y -q install --no-install-recommends lightdm lightdm-gtk-greeter-settings && \
    \
    # Alguns aplicativos do Gnome
    apt -y -q install --no-install-recommends network-manager-gnome gparted gnome-calculator gnome-disk-utility gnome-software-plugin-flatpak && \
    \
    # Alguns aplicativos do MATE
    apt -y -q install --no-install-recommends mate-system-monitor engrampa pluma && \
    \
    # Alguns aplicativos do KDE
    apt -y -q install --no-install-recommends okular kcolorchooser && \
    \
    # Adicionando Backports para o LibreOffice
    echo "deb http://debian.pop-sc.rnp.br/debian stretch-backports main contrib non-free" > /etc/apt/sources.list.d/stretch-backports.list && \
    apt update && \
    \
    # Instalando o LibreOffice e compilador de Go
    apt -y -q install -t stretch-backports libreoffice libreoffice-l10n-pt-br libreoffice-help-pt-br libreoffice-officebean libreoffice-avmedia-backend-vlc libreoffice-gtk3 libreoffice-pdfimport libreoffice-subsequentcheckbase golang hplip hplip-data && \
    \
    # Comentando Backport
    echo "# deb http://debian.pop-sc.rnp.br/debian stretch-backports main contrib non-free" > /etc/apt/sources.list.d/stretch-backports.list && \
    \
    # Adicionando chaves de repositorios
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 931FF8E79F0876134EDDBDCCA87FF9DF48BF1C90 && \
    wget -O - https://download.videolan.org/pub/debian/videolan-apt.asc | apt-key add - && \
    wget -O - https://download.opensuse.org/repositories/shells:fish:release:3/Debian_9.0/Release.key | apt-key add - && \
    wget -q "http://deb.playonlinux.com/public.gpg" -O- | apt-key add - && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 73C3DB2A && \
    \
    # Adicionando repositorios do Spotify, Video Lan Center e FISH
    echo "deb https://download.videolan.org/pub/debian/stable/ /" > /etc/apt/sources.list.d/video-lan-center.list && \
    echo "deb http://repository.spotify.com stable non-free" > /etc/apt/sources.list.d/spotify.list && \
    echo 'deb http://download.opensuse.org/repositories/shells:/fish:/release:/3/Debian_9.0/ /' > /etc/apt/sources.list.d/shells:fish:release:3.list && \
    wget http://deb.playonlinux.com/playonlinux_stretch.list -O /etc/apt/sources.list.d/playonlinux.list && \
    echo "deb http://ppa.launchpad.net/linuxuprising/java/ubuntu bionic main" >> /etc/apt/sources.list.d/java-11-oracle.list && \
    apt update && \
    \
    # Instalando pacotes da interface grafica em si e a biblioteca de DVD libdvdcss2
    apt -y -q install spotify-client xfce4 xfce4-goodies xfce4-screenshooter xfce4-notes-plugin xfce4-terminal xfce4-datetime-plugin xfce4-topmenu-plugin xfce4-whiskermenu-plugin libappindicator1 albatross-gtk-theme arc-theme xscreensaver libdvdcss2 breeze-icon-theme breeze-cursor-theme fish thunar-dropbox-plugin playonlinux && \
    \
    # Adicionar repositorio flathub ao flatpak
    flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo && \
    \
    # Instalando o tema Adapta
    wget jpsmb.sj.ifsc.edu.br/adapta.tar.xz -O /adapta.tar.xz && \
    tar -xvf /adapta.tar.xz -C /usr/share/themes/ && \
    rm -r /adapta.tar.xz && \
    \
    # Fonte Open Sans
    wget "https://fonts.google.com/download?family=Open%20Sans|Open%20Sans%20Condensed" -O open-sans.zip && \
    unzip open-sans.zip -d /usr/share/fonts/opentype/ && \
    rm -f open-sans.zip && \
    \
    # Instalar o Webmin
    rm /etc/apt/apt.conf.d/docker-gzip-indexes && \
    rm /var/lib/apt/lists/*lz4 && \
    apt-get -o Acquire::GzipIndexes=false update && \
    apt -y -q install libauthen-pam-perl apt-show-versions && \
    wget https://ufpr.dl.sourceforge.net/project/webadmin/webmin/1.910/webmin_1.910_all.deb -O /webmin.deb && \
    dpkg -i /webmin.deb && \
    rm -r /webmin.deb && \
    apt update && \
    \
    # Configurar o VIM
    echo -n "set number\nsy on\nset paste\nset background=dark" > /root.vimrc && \
    \
    # Desktop do Equalizador do Pulseaudio
    echo "[Desktop Entry]" > /usr/share/applications/pulseaudio-equalizer.desktop && \
    echo "Version=1.0" >> /usr/share/applications/pulseaudio-equalizer.desktop && \
    echo "Encoding=UTF-8" >> /usr/share/applications/pulseaudio-equalizer.desktop && \
    echo "Name=PulseAudio Equalizer" >> /usr/share/applications/pulseaudio-equalizer.desktop && \
    echo "GenericName=Equalizer" >> /usr/share/applications/pulseaudio-equalizer.desktop && \
    echo "Comment=PulseAudio" >> /usr/share/applications/pulseaudio-equalizer.desktop && \
    echo "Exec=qpaeq" >> /usr/share/applications/pulseaudio-equalizer.desktop && \
    echo "Icon=multimedia-volume-control" >> /usr/share/applications/pulseaudio-equalizer.desktop && \
    echo "StartupNotify=true" >> /usr/share/applications/pulseaudio-equalizer.desktop && \
    echo "Type=Application" >> /usr/share/applications/pulseaudio-equalizer.desktop && \
    echo "Categories=AudioVideo;Audio;Mixer;GTK;" >> /usr/share/applications/pulseaudio-equalizer.desktop && \
    \
    # Criando terminalrc no skel
    mkdir -p /etc/skel/.config/xfce4/terminal/ && \
    echo "[Configuration]" > /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "FontName=NotoMono Nerd Font 12" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscAlwaysShowTabs=FALSE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscBell=FALSE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscBellUrgent=FALSE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscBordersDefault=TRUE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscCursorBlinks=FALSE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscCursorShape=TERMINAL_CURSOR_SHAPE_BLOCK" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscDefaultGeometry=80x24" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscInheritGeometry=FALSE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscMenubarDefault=TRUE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscMouseAutohide=FALSE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscMouseWheelZoom=TRUE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscToolbarDefault=FALSE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscConfirmClose=TRUE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscCycleTabs=TRUE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscTabCloseButtons=TRUE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscTabCloseMiddleClick=TRUE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscTabPosition=GTK_POS_TOP" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscHighlightUrls=TRUE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscMiddleClickOpensUri=FALSE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscCopyOnSelect=FALSE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscDefaultWorkingDir=" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscRewrapOnResize=TRUE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscUseShiftArrowsToScroll=FALSE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "MiscSlimTabs=FALSE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "ScrollingUnlimited=TRUE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    echo "ScrollingOnOutput=FALSE" >> /etc/skel/.config/xfce4/terminal/terminalrc && \
    \
    # Definindo o layout de teclado para ABNT 2
    mkdir -p /etc/skel/.config/xfce4/xfconf/xfce-perchannel-xml/ && \
    echo '<?xml version="1.0" encoding="UTF-8"?>' > /etc/skel/.config/xfce4/xfconf/xfce-perchannel-xml/keyboard-layout.xml && \
    echo '' >> /etc/skel/.config/xfce4/xfconf/xfce-perchannel-xml/keyboard-layout.xml && \
    echo '<channel name="keyboard-layout" version="1.0">' >> /etc/skel/.config/xfce4/xfconf/xfce-perchannel-xml/keyboard-layout.xml && \
    echo '  <property name="Default" type="empty">' >> /etc/skel/.config/xfce4/xfconf/xfce-perchannel-xml/keyboard-layout.xml && \
    echo '    <property name="XkbDisable" type="bool" value="false"/>' >> /etc/skel/.config/xfce4/xfconf/xfce-perchannel-xml/keyboard-layout.xml && \
    echo '    <property name="XkbLayout" type="string" value="br"/>' >> /etc/skel/.config/xfce4/xfconf/xfce-perchannel-xml/keyboard-layout.xml && \
    echo '    <property name="XkbVariant" type="string" value=""/>' >> /etc/skel/.config/xfce4/xfconf/xfce-perchannel-xml/keyboard-layout.xml && \
    echo '  </property>' >> /etc/skel/.config/xfce4/xfconf/xfce-perchannel-xml/keyboard-layout.xml && \
    echo '</channel>' >> /etc/skel/.config/xfce4/xfconf/xfce-perchannel-xml/keyboard-layout.xml && \
    \
    # Remover o pacote light-locker para previnir que a tela deixe de ser exibida ao retornar no bloqueio do lightdm
    apt -y -q purge light-locker && \
    \
    # Fazendo uma limpeza
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/log/* /root/.bash_history && \
    rm -rf /etc/ssh/*key* && \
    \
    # Gambiarra para o ps
    ln -s /bin/ps /usr/bin/ps && \
    \
    # Carregar modulos para o Equalizador do Pulseaudio
    echo "" >> /etc/pulse/default.pa && \
    echo "load-module module-equalizer-sink" >> /etc/pulse/default.pa && \
    echo "load-module module-dbus-protocol" >> /etc/pulse/default.pa && \
    \
    # Truque do UDEV para impedir nomes longos em adaptadores Wi-Fi
    ln -s /dev/null /etc/udev/rules.d/80-net-setup-link.rules && \
    \
    # Criando usuarios
    addgroup --gid 1100 rancher && \
    addgroup --gid 1101 docker && \
    useradd -u 1100 -g rancher -G docker,sudo,plugdev,dialout,audio,video,netdev -c "Rancher,,," -m -s /bin/bash rancher && \
    useradd -u 1101 -g docker -G docker,sudo -c "Docker,,," -m -s /bin/bash docker && \
    echo ClientAliveInterval 180 >> /etc/ssh/sshd_config && \
    echo '## allow password less for rancher user' >> /etc/sudoers && \
    echo 'rancher ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers && \
    echo '## allow password less for docker user' >> /etc/sudoers && \
    echo 'docker ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers && \
    echo '## allow password less execution of nm-applet as a privileged user' >> /etc/sudoers && \
    echo 'ALL ALL=(ALL) NOPASSWD: /usr/bin/nm-applet' >> /etc/sudoers && \
    echo 'ALL ALL=(ALL) NOPASSWD: /usr/bin/nm-connection-editor' >> /etc/sudoers && \
    \
    # Ajustes no libvirt, adduser, autostart do nm-applet
    sed -i '105s/.*/greeter-hide-users=false/' /etc/lightdm/lightdm.conf && \
    sed -i '85s/.*/unix_sock_group = "rancher"/' /etc/libvirt/libvirtd.conf && \
    sed -i '102s/.*/unix_sock_rw_perms = "0770"/' /etc/libvirt/libvirtd.conf && \
    sed -i '6s:.*:DSHELL=/usr/bin/fish:' /etc/adduser.conf && \
    sed -i '77s:.*:EXTRA_GROUPS="dialout cdrom audio video plugdev netdev":' /etc/adduser.conf && \
    sed -i '81s:.*:ADD_EXTRA_GROUPS=1:' /etc/adduser.conf && \
    sed -i 's.Exec=nm-applet.Exec=sh -c "sudo nm-applet".g' /etc/xdg/autostart/nm-applet.desktop && \
    sed -i 's.Exec=nm-connection-editor.Exec=sh -c "sudo nm-connection-editor".g' /usr/share/applications/nm-connection-editor.desktop && \
    sed -i 's.; default-sample-format = s16le.default-sample-format = float32le.g' /etc/pulse/daemon.conf && \
    \
    # Regras para o Network-Manager
    echo "[nm-applet]" > /etc/polkit-1/localauthority/10-vendor.d/org.freedesktop.NetworkManager.pkla && \
    echo "Identity=unix-group:netdev" >> /etc/polkit-1/localauthority/10-vendor.d/org.freedesktop.NetworkManager.pkla && \
    echo "Action=org.freedesktop.NetworkManager.enable-disable-network;org.freedesktop.NetworkManager.enable-disable-wifi;org.freedesktop.NetworkManager.enable-disable-wwan;org.freedesktop.NetworkManager.enable-disable-wimax;org.freedesktop.NetworkManager.network-control;org.freedesktop.NetworkManager.wifi.share.protected;org.freedesktop.NetworkManager.wifi.share.open;org.freedesktop.NetworkManager.settings.modify.own;org.freedesktop.NetworkManager.enable-disable-statistics" >> /etc/polkit-1/localauthority/10-vendor.d/org.freedesktop.NetworkManager.pkla && \
    echo "ResultActive=yes" >> /etc/polkit-1/localauthority/10-vendor.d/org.freedesktop.NetworkManager.pkla && \
    echo "ResultAny=yes" >> /etc/polkit-1/localauthority/10-vendor.d/org.freedesktop.NetworkManager.pkla && \
    echo "ResultInactive=no" >> /etc/polkit-1/localauthority/10-vendor.d/org.freedesktop.NetworkManager.pkla && \
    \
    # Regras para montagem
    echo "[Mount a system-internal device]" > /etc/polkit-1/localauthority/50-local.d/50-mount.pkla && \
    echo "Identity=unix-group:plugdev" >> /etc/polkit-1/localauthority/50-local.d/50-mount.pkla && \
    echo "Action=org.freedesktop.udisks2.filesystem-mount;org.freedesktop.udisks2.encrypted-unlock;org.freedesktop.udisks2.encrypted-change-passphrase;org.freedesktop.udisks2.loop-setup;org.freedesktop.udisks2.power-off-drive;org.freedesktop.udisks2.eject-media;org.freedesktop.udisks2.modify-device;org.freedesktop.udisks2.rescan;org.freedesktop.udisks2.ata-smart-update;org.freedesktop.udisks2.ata-check-power;org.freedesktop.udisks2.ata-standby;org.freedesktop.udisks2.cancel-job" >> /etc/polkit-1/localauthority/50-local.d/50-mount.pkla && \
    echo "ResultAny=yes" >> /etc/polkit-1/localauthority/50-local.d/50-mount.pkla && \
    echo "ResultActive=yes" >> /etc/polkit-1/localauthority/50-local.d/50-mount.pkla && \
    echo "ResultInactive=no" >> /etc/polkit-1/localauthority/50-local.d/50-mount.pkla && \ 
    \
    # Regra para desligar e reiniciar o sistema
    echo "[XFCE Session]" > /etc/polkit-1/localauthority/50-local.d/20-xfce-session.pkla && \
    echo "Identity=unix-group:*" >> /etc/polkit-1/localauthority/50-local.d/20-xfce-session.pkla && \
    echo "Action=org.xfce.session.xfsm-shutdown-helper" >> /etc/polkit-1/localauthority/50-local.d/20-xfce-session.pkla && \
    echo "ResultActive=yes" >> /etc/polkit-1/localauthority/50-local.d/20-xfce-session.pkla && \
    echo "ResultAny=yes" >> /etc/polkit-1/localauthority/50-local.d/20-xfce-session.pkla && \
    echo "ResultInactive=no" >> /etc/polkit-1/localauthority/50-local.d/20-xfce-session.pkla && \
    \
    # Regra para ajustar o brilho da tela
    echo "[XFCE Backlight]" > /etc/polkit-1/localauthority/50-local.d/21-xfce-power.pkla && \
    echo "Identity=unix-group:*" >> /etc/polkit-1/localauthority/50-local.d/21-xfce-power.pkla && \
    echo "Action=org.xfce.power.backlight-helper;org.xfce.power.xfce4-pm-helper" >> /etc/polkit-1/localauthority/50-local.d/21-xfce-power.pkla && \
    echo "ResultActive=yes" >> /etc/polkit-1/localauthority/50-local.d/21-xfce-power.pkla && \
    echo "ResultAny=yes" >> /etc/polkit-1/localauthority/50-local.d/21-xfce-power.pkla && \
    echo "ResultInactive=no" >> /etc/polkit-1/localauthority/50-local.d/21-xfce-power.pkla && \
    \
    # Regra para ajuste de brilho da tela para Intel
    echo "[Intel backlight]" > /etc/polkit-1/localauthority/50-local.d/22-org.x.xf86-video-intel.backlight-helper.pkla && \
    echo "Identity=unix-group:*" >> /etc/polkit-1/localauthority/50-local.d/22-org.x.xf86-video-intel.backlight-helper.pkla && \
    echo "Action=org.x.xf86-video-intel.backlight-helper" >> /etc/polkit-1/localauthority/50-local.d/22-org.x.xf86-video-intel.backlight-helper.pkla && \
    echo "ResultActive=yes" >> /etc/polkit-1/localauthority/50-local.d/22-org.x.xf86-video-intel.backlight-helper.pkla && \
    echo "ResultAny=yes" >> /etc/polkit-1/localauthority/50-local.d/22-org.x.xf86-video-intel.backlight-helper.pkla && \
    echo "ResultInactive=no" >> /etc/polkit-1/localauthority/50-local.d/22-org.x.xf86-video-intel.backlight-helper.pkla && \
    \
    # Regra para o login1
    echo "[Login1]" > /etc/polkit-1/localauthority/50-local.d/23-org.freedesktop.login1.pkla && \
    echo "Identity=unix-group:*" >> /etc/polkit-1/localauthority/50-local.d/23-org.freedesktop.login1.pkla && \
    echo "Action=org.freedesktop.login1.inhibit-block-shutdown;org.freedesktop.login1.inhibit-block-sleep;org.freedesktop.login1.inhibit-handle-power-key;org.freedesktop.login1.inhibit-handle-suspend-key;org.freedesktop.login1.inhibit-handle-hibernate-key;org.freedesktop.login1.inhibit-handle-lid-switch;org.freedesktop.login1.power-off;org.freedesktop.login1.power-off-multiple-sessions;org.freedesktop.login1.reboot;org.freedesktop.login1.reboot-multiple-sessions;org.freedesktop.login1.suspend-multiple-sessions;org.freedesktop.login1.hibernate;org.freedesktop.login1.hibernate-multiple-sessions" >> /etc/polkit-1/localauthority/50-local.d/23-org.freedesktop.login1.pkla && \
    echo "ResultActive=yes" >> /etc/polkit-1/localauthority/50-local.d/23-org.freedesktop.login1.pkla && \
    echo "ResultAny=yes" >> /etc/polkit-1/localauthority/50-local.d/23-org.freedesktop.login1.pkla && \
    echo "ResultInactive=no" >> /etc/polkit-1/localauthority/50-local.d/23-org.freedesktop.login1.pkla && \
    \ 
    # Habilitando o toque no touchpad
    mkdir /etc/X11/xorg.conf.d/ && \
    echo 'Section "InputClass"' > /etc/X11/xorg.conf.d/40-libinput.conf && \
    echo '        Identifier "libinput touchpad catchall"' >> /etc/X11/xorg.conf.d/40-libinput.conf && \
    echo '        MatchIsTouchpad "on"' >> /etc/X11/xorg.conf.d/40-libinput.conf && \
    echo '        MatchDevicePath "/dev/input/event*"' >> /etc/X11/xorg.conf.d/40-libinput.conf && \
    echo '        Driver "libinput"' >> /etc/X11/xorg.conf.d/40-libinput.conf && \
    echo '        Option "Tapping" "on"' >> /etc/X11/xorg.conf.d/40-libinput.conf && \
    echo '        Option "HorizontalScrolling" "0"' >> /etc/X11/xorg.conf.d/40-libinput.conf && \
    echo 'EndSection' >> /etc/X11/xorg.conf.d/40-libinput.conf && \
    \
    # Ajuste no horario e idioma
    echo "America/Sao_Paulo" > /etc/timezone && \
    rm -r /etc/localtime && \
    ln -snf /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata && \
    echo "pt_BR.UTF-8 UTF-8" > /etc/locale.gen && \
    echo 'LANG="pt_BR.UTF-8"' > /etc/default/locale && \
    dpkg-reconfigure -f noninteractive locales && \
    update-locale LANG=pt_BR.UTF-8 && \
    echo 'export LANG=pt_BR.UTF-8' >> /etc/profile && \
    echo 'setxkbmap br' >> /etc/profile && \
    locale-gen --purge en_US.UTF-8 && \
    bash -c "echo -e 'LANG="pt_BR.UTF-8"\nLANGUAGE="pt_BR:br"\n'" > /etc/default/locale && \
    \
    # Adicionando a logo do RancherOS quando se faz SSH
    echo -n "#!/bin/bash\n\ncat << \EOF\n               ,        , ______                 _                 _____ _____TM\n  ,------------|'------'| | ___ \               | |               /  _  /  ___|\n / .           '-'    |-  | |_/ /__ _ _ __   ___| |__   ___ _ __  | | | \ '--.\n \/|             |    |   |    // _' | '_ \ / __| '_ \ / _ \ '__' | | | |'--. \ \n   |   .________.'----'   | |\ \ (_| | | | | (__| | | |  __/ |    | \_/ /\__/ /\n   |   |        |   |     \_| \_\__,_|_| |_|\___|_| |_|\___|_|     \___/\____/\nEOF\n\ncat << EOF\n   \___/        \___/     Linux \$(uname -r)\n\n         RancherOS \$(uname -v) \$(hostname)\nEOF" > /etc/update-motd.d/00-header && \
    chmod +x /etc/update-motd.d/00-header && \
    \
    # Adicionando a logo do RancherOS quando executa um novo BASH
    echo -n "\n/etc/update-motd.d/00-header" >> /etc/bash.bashrc && \
    \
    # Adicionando a logo do RancherOS quando executa um novo FISH
    echo -n "\nfunction fish_greeting\n    bash /etc/update-motd.d/00-header\nend" >> /etc/fish/config.fish && \
    \
    # Criando script que toca em /dev/sr0
    echo -n "#!/bin/bash\n\nwhile (true);do\n    touch /dev/sr0\n    sleep 1\ndone" > /usr/local/bin/tocar-sr0 && \
    chmod 100 /usr/local/bin/tocar-sr0 && \
    \
    # Desabilitando o travamento do CD pelo kernel
    echo "sys.dev.cdrom.lock=0" >> /etc/sysctl.conf && \
    \
    # Zerando a variavel DEBIAN_FRONTEND
    unset DEBIAN_FRONTEND && \
    \
    # Script que inicia todo o conjunto necessario para o bom funcionamento do console
    echo "#!/bin/bash" > /usr/local/bin/iniciar-tudo && \
    echo "" >> /usr/local/bin/iniciar-tudo && \
    echo "mount -o remount,size=1G /dev/shm" >> /usr/local/bin/iniciar-tudo && \
    echo "rm -r /tmp/.X0-lock /tmp/.X11-unix" >> /usr/local/bin/iniciar-tudo && \
    echo "/usr/local/bin/tocar-sr0 &" >> /usr/local/bin/iniciar-tudo && \
    echo "service dbus start" >> /usr/local/bin/iniciar-tudo && \
    echo "service udev start" >> /usr/local/bin/iniciar-tudo && \
    echo "service rsyslog start" >> /usr/local/bin/iniciar-tudo && \
    echo "service libvirtd start" >> /usr/local/bin/iniciar-tudo && \
    echo "service libvirt-guests start" >> /usr/local/bin/iniciar-tudo && \
    echo "service virtlogd start" >> /usr/local/bin/iniciar-tudo && \
    echo "service webmin start" >> /usr/local/bin/iniciar-tudo && \
    echo "service network-manager start" >> /usr/local/bin/iniciar-tudo && \
    echo "service cups start" >> /usr/local/bin/iniciar-tudo && \
    echo "service cups-browsed start" >> /usr/local/bin/iniciar-tudo && \
    echo "modprobe -r evbug" >> /usr/local/bin/iniciar-tudo && \
    echo 'echo "0 2147483647" > /proc/sys/net/ipv4/ping_group_range' >> /usr/local/bin/iniciar-tudo && \
    echo "cron" >> /usr/local/bin/iniciar-tudo && \
    echo "ntpd" >> /usr/local/bin/iniciar-tudo && \
    echo 'sleep 2 && bash -c "/etc/init.d/lightdm start" &' >> /usr/local/bin/iniciar-tudo && \
    echo "ros console-init" >> /usr/local/bin/iniciar-tudo && \
    \
    # Alterando as permissoes do script de inicio
    chmod 100 /usr/local/bin/iniciar-tudo

ENTRYPOINT ["/usr/bin/ros", "entrypoint"]
