Dockerfile
FROM kalilinux/kali-rolling

ENV DEBIAN_FRONTEND=noninteractive

# Paquetes esenciales: XFCE, temas, fondos oficiales, Burp Suite, Wordlists, red y feh
RUN apt-get update && apt-get install -y --no-install-recommends \
    kali-linux-core \
    kali-tools-top10 \
    kali-desktop-xfce \
    kali-themes \
    kali-wallpapers-all \
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
    feh \
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

# Configurar arranque de VNC cargando directamente el wallpaper oficial con feh
RUN mkdir -p /home/kali/.vnc && \
    echo "kali123" | vncpasswd -f > /home/kali/.vnc/passwd && \
    chmod 600 /home/kali/.vnc/passwd && \
    printf '#!/bin/sh\nunset SESSION_MANAGER\nunset DBUS_SESSION_BUS_ADDRESS\nautocutsel -fork -selection CLIPBOARD\nautocutsel -fork -selection PRIMARY\nfeh --bg-fill /usr/share/backgrounds/kali-16x9/default.png &\nexec startxfce4\n' > /home/kali/.vnc/xstartup && \
    chmod +x /home/kali/.vnc/xstartup
