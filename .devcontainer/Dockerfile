Dockerfile
FROM kalilinux/kali-rolling

ENV DEBIAN_FRONTEND=noninteractive

# Instalar escritorio XFCE, temas oficiales, fondos, herramientas y VNC
RUN apt-get update && apt-get install -y --no-install-recommends \
    kali-linux-core \
    kali-tools-top10 \
    kali-desktop-xfce \
    kali-themes \
    kali-wallpapers-2024 \
    burpsuite \
    wordlists \
    iputils-ping \
    net-tools \
    dnsutils \
    iproute2 \
    firefox-esr \
    autocutsel \
    xfonts-base \
    openvpn \
    iptables \
    tightvncserver \
    tigervnc-tools \
    novnc \
    websockify \
    sudo \
    curl \
    ca-certificates \
    procps \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Redirigir la raíz web a noVNC
RUN ln -s /usr/share/novnc/vnc.html /usr/share/novnc/index.html

# Configurar usuario estándar 'kali'
RUN useradd -m -s /bin/bash kali && \
    echo "kali:kali" | chpasswd && \
    adduser kali sudo && \
    echo "kali ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER kali
ENV USER=kali
WORKDIR /home/kali

# Configurar contraseña de VNC y xstartup
RUN mkdir -p /home/kali/.vnc && \
    echo "kali123" | vncpasswd -f > /home/kali/.vnc/passwd && \
    chmod 600 /home/kali/.vnc/passwd && \
    echo '#!/bin/sh\nunset SESSION_MANAGER\nunset DBUS_SESSION_BUS_ADDRESS\nautocutsel -fork -selection CLIPBOARD\nautocutsel -fork -selection PRIMARY\nexec startxfce4' > /home/kali/.vnc/xstartup && \
    chmod +x /home/kali/.vnc/xstartup

# Forzar el fondo de pantalla oficial en la configuración de XFCE
RUN mkdir -p /home/kali/.config/xfce4/xfconf/xfce-perchannel-xml && \
    echo '<?xml version="1.0" encoding="UTF-8"?>\n<channel name="xfce4-desktop" version="1.0">\n  <property name="backdrop" type="empty">\n    <property name="screen0" type="empty">\n      <property name="monitor0" type="empty">\n        <property name="workspace0" type="empty">\n          <property name="last-image" type="string" value="/usr/share/backgrounds/kali/kali-dragon-16x9.svg"/>\n          <property name="image-style" type="int" value="5"/>\n        </property>\n      </property>\n    </property>\n  </property>\n</channel>' > /home/kali/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-desktop.xml
