FROM kalilinux/kali-rolling

ENV DEBIAN_FRONTEND=noninteractive

# Instalar herramientas esenciales de Kali, escritorio XFCE, temas visuales y servidor web noVNC
RUN apt-get update && apt-get install -y --no-install-recommends \
    kali-linux-core \
    kali-tools-top10 \
    kali-themes \
    kali-wallpapers-all \
    xfce4 \
    xfce4-terminal \
    dbus-x11 \
    tightvncserver \
    tigervnc-tools \
    xfonts-base \
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

# Preconfigurar arranque del entorno de escritorio XFCE
RUN mkdir -p /home/kali/.vnc && \
    echo "kali123" | vncpasswd -f > /home/kali/.vnc/passwd && \
    chmod 600 /home/kali/.vnc/passwd && \
    echo '#!/bin/sh\nunset SESSION_MANAGER\nunset DBUS_SESSION_BUS_ADDRESS\nexec startxfce4' > /home/kali/.vnc/xstartup && \
    chmod +x /home/kali/.vnc/xstartup
