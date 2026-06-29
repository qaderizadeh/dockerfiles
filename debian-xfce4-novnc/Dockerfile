FROM debian

ENV DEBIAN_FRONTEND=noninteractive

# Install core system
RUN apt update && apt install -y \
    xfce4 \
    xfce4-terminal \
    dbus-x11 \
    tigervnc-standalone-server \
    novnc \
    websockify \
    sudo \
    bash \
    curl \
    && apt clean && rm -rf /var/lib/apt/lists/*

# Create user
RUN useradd -m -s /bin/bash devuser && \
    echo "devuser:devpass" | chpasswd && \
    adduser devuser sudo

# VNC setup directory
RUN mkdir -p /home/devuser/.vnc && \
    chown -R devuser:devuser /home/devuser/.vnc

# Set VNC password (for devuser)
RUN echo "123456" | vncpasswd -f > /home/devuser/.vnc/passwd && \
    chown devuser:devuser /home/devuser/.vnc/passwd && \
    chmod 600 /home/devuser/.vnc/passwd

# XFCE startup script
RUN echo '#!/bin/bash\n\
unset SESSION_MANAGER\n\
unset DBUS_SESSION_BUS_ADDRESS\n\
exec dbus-launch --exit-with-session startxfce4' \
> /home/devuser/.vnc/xstartup && \
    chmod +x /home/devuser/.vnc/xstartup && \
    chown devuser:devuser /home/devuser/.vnc/xstartup

EXPOSE 5901 6080

# Switch to user
USER devuser
WORKDIR /home/devuser

# Start everything
CMD bash -c "\
vncserver :1 -geometry 1280x720 -depth 24 && \
websockify --web=/usr/share/novnc/ 6080 localhost:5901"
