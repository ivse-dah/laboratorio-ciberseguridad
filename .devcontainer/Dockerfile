FROM kalilinux/kali-rolling

ENV DEBIAN_FRONTEND=noninteractive

# Instalar escritorio XFCE, noVNC y herramientas esenciales
RUN apt-get update && apt-get install -y --no-install-recommends \
    kali-linux-core \
    kali-tools-top10 \
    xfce4 \
    xfce4-terminal \
    dbus-x11 \
    tightvncserver \
    tigervnc-tools \
    novnc \
    websockify \
    sudo \
    curl \
    ca-certificates \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Configurar usuario kali con permisos sudo
RUN useradd -m -s /bin/bash kali && \
    echo "kali:kali" | chpasswd && \
    adduser kali sudo && \
    echo "kali ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER kali
WORKDIR /home/kali

# Preconfigurar arranque del entorno de escritorio XFCE
RUN mkdir -p /home/kali/.vnc && \
    echo "kali123" | vncpasswd -f > /home/kali/.vnc/passwd && \
    chmod 600 /home/kali/.vnc/passwd && \
    echo '#!/bin/sh\nunset SESSION_MANAGER\nunset DBUS_SESSION_BUS_ADDRESS\nexec startxfce4' > /home/kali/.vnc/xstartup && \
    chmod +x /home/kali/.vnc/xstartup
