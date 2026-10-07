FROM kalilinux/kali-rolling

ENV DEBIAN_FRONTEND=noninteractive

# Paquetes completos con temas oficiales y herramientas solicitadas
RUN apt-get update && apt-get install -y \
    kali-linux-core \
    kali-tools-top10 \
    kali-desktop-xfce \
    kali-themes \
    kali-wallpapers-2024 \
    burpsuite \
    wordlists \
    enum4linux \
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

# Redirigir raíz web directo a noVNC
RUN ln -s /usr/share/novnc/vnc.html /usr/share/novnc/index.html

# Crear usuario estándar 'kali'
RUN useradd -m -s /bin/bash kali && \
    echo "kali:kali" | chpasswd && \
    adduser kali sudo && \
    echo "kali ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER kali
ENV USER=kali
WORKDIR /home/kali

# Configuración del servidor VNC y arranque limpio de la sesión gráfica oficial
RUN mkdir -p /home/kali/.vnc && \
    echo "kali123" | vncpasswd -f > /home/kali/.vnc/passwd && \
    chmod 600 /home/kali/.vnc/passwd && \
    printf '#!/bin/sh\nunset SESSION_MANAGER\nunset DBUS_SESSION_BUS_ADDRESS\nautocutsel -fork -selection CLIPBOARD\nautocutsel -fork -selection PRIMARY\n/etc/X11/Xsession\n' > /home/kali/.vnc/xstartup && \
    chmod +x /home/kali/.vnc/xstartup
