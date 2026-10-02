FROM kalilinux/kali-rolling

# Evitar prompts interactivos durante la instalación
ENV DEBIAN_FRONTEND=noninteractive

# Instalar escritorio XFCE, servidor noVNC y paquete esencial de Kali
RUN apt-get update && apt-get install -y --no-install-recommends \
    kali-linux-core \
    kali-tools-top10 \
    xfce4 \
    xfce4-terminal \
    novnc \
    websockify \
    tigervnc-standalone-server \
    sudo \
    curl \
    ca-certificates \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Crear usuario estándar sin privilegios de root directos
RUN useradd -m -s /bin/bash kali && \
    echo "kali:kali" | chpasswd && \
    adduser kali sudo && \
    echo "kali ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER kali
WORKDIR /home/kali

# Script de arranque del escritorio web noVNC en el puerto 6080
CMD ["sh", "-c", "vncserver :1 -geometry 1280x720 -depth 24 && websockify --web /usr/share/novnc/ 6080 localhost:5901"]
