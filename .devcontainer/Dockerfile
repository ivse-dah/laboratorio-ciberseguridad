FROM kalilinux/kali-rolling

ENV DEBIAN_FRONTEND=noninteractive

# Instalar entorno XFCE oficial, utilidades de red, Firefox, OpenVPN, Burp Suite y Wordlists
RUN apt-get update && apt-get install -y \
    kali-linux-core \
    kali-tools-top10 \
    kali-desktop-xfce \
    kali-wallpapers-all \
    burpsuite \
    wordlists \
    default-jre \
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
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Redirigir la raíz web directo al visor VNC
RUN ln -s /usr/share/novnc/vnc.html /usr/share/novnc/index.html

# Configurar usuario estándar 'kali' con permisos sudo
RUN useradd -m -s /bin/bash kali && \
    echo "kali:kali" | chpasswd && \
    adduser kali sudo && \
    echo "kali ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER kali
ENV USER=kali
WORKDIR /home/kali

# Preconfigurar arranque del entorno de escritorio XFCE con portapapeles activo
RUN mkdir -p /home/kali/.vnc && \
    echo "kali123" | vncpasswd -f > /home/kali/.vnc/passwd && \
    chmod 600 /home/kali/.vnc/passwd && \
    echo '#!/bin/sh\nunset SESSION_MANAGER\nunset DBUS_SESSION_BUS_ADDRESS\nautocutsel -fork -selection CLIPBOARD\nautocutsel -fork -selection PRIMARY\nexec startxfce4' > /home/kali/.vnc/xstartup && \
    chmod +x /home/kali/.vnc/xstartup
