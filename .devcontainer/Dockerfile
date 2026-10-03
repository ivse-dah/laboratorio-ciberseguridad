FROM kalilinux/kali-rolling

ENV DEBIAN_FRONTEND=noninteractive

# Paquetes esenciales con temas completos de Kali
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

# Configuración clásica de XFCE en VNC tal cual la teníamos antes
RUN mkdir -p /home/kali/.vnc && \
    echo "kali123" | vncpasswd -f > /home/kali/.vnc/passwd && \
    chmod 600 /home/kali/.vnc/passwd && \
    printf '#!/bin/sh\nunset SESSION_MANAGER\nunset DBUS_SESSION_BUS_ADDRESS\nautocutsel -fork -selection CLIPBOARD\nautocutsel -fork -selection PRIMARY\nstartxfce4 &\n' > /home/kali/.vnc/xstartup && \
    chmod +x /home/kali/.vnc/xstartup
