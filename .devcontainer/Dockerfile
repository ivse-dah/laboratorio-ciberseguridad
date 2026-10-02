FROM kalilinux/kali-rolling

ENV DEBIAN_FRONTEND=noninteractive

# Paquetes completos: escritorio oficial, fondos, herramientas solicitadas y red
RUN apt-get update && apt-get install -y \
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

# Configuración del entorno gráfico con sesión y portapapeles
RUN mkdir -p /home/kali/.vnc && \
    echo "kali123" | vncpasswd -f > /home/kali/.vnc/passwd && \
    chmod 600 /home/kali/.vnc/passwd && \
    echo '#!/bin/sh\nunset SESSION_MANAGER\nunset DBUS_SESSION_BUS_ADDRESS\nautocutsel -fork -selection CLIPBOARD\nautocutsel -fork -selection PRIMARY\nexec startxfce4' > /home/kali/.vnc/xstartup && \
    chmod +x /home/kali/.vnc/xstartup

# Script de arranque persistente: inicia VNC + noVNC y se queda en escucha para que NO se apague nunca
USER root
RUN echo '#!/bin/bash\nsu - kali -c "vncserver -kill :1 2>/dev/null; vncserver :1 -geometry 1280x720 -depth 24"\nsu - kali -c "websockify -D --web /usr/share/novnc/ 6080 localhost:5901"\ntail -f /dev/null' > /entrypoint.sh && \
    chmod +x /entrypoint.sh

USER kali
ENTRYPOINT ["/entrypoint.sh"]
