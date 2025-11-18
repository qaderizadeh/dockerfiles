FROM debian

# Update and install required packages
RUN apt update -y
RUN DEBIAN_FRONTEND=noninteractive apt install -y \
    bash \
    git \
    xfce4 \
    xfce4-terminal \
    dbus-x11 \
    python3 \
    tightvncserver \
    sudo

# Clone noVNC and websockify repositories
RUN git clone https://github.com/novnc/noVNC.git /opt/noVNC
RUN git clone https://github.com/novnc/websockify.git /opt/noVNC/utils/websockify

# Create user 'debian' and setup password + sudo
RUN useradd -ms /bin/bash debian
RUN echo "debian:debian" | chpasswd
RUN adduser debian sudo

# Switch to debian user
USER debian
WORKDIR /home/debian

# VNC password setup
RUN mkdir ~/.vnc
RUN echo -ne '\xb3\x82\xfe\x6f\xf8\xac\xd1\xa9' > ~/.vnc/passwd
RUN chmod 400 ~/.vnc/passwd

# VNC xstartup configuration
RUN printf '#!/bin/bash\nstartxfce4 &' > ~/.vnc/xstartup
RUN chmod +x ~/.vnc/xstartup

# Start VNC server and noVNC proxy
CMD rm -f /tmp/.X1-lock /tmp/.X11-unix/X1 ; \
    USER=debian vncserver -kill :1 ; \
    USER=debian vncserver :1 && \
    /opt/noVNC/utils/novnc_proxy --vnc localhost:5901

# --------------------------------------------------------------------------------------------------
# CRITICAL POST-RUN INSTRUCTIONS FOR SECURITY AND STABILITY:
# --------------------------------------------------------------------------------------------------
# 1. BUILD:   docker build -t debian-xfce4-novnc .
# 2. RUN:     docker run -d -p 5901:5901 -p 6080:6080 --name debian-desktop debian-xfce4-novnc
# 3. SECURE:  The default password is INSECURE. You MUST change it immediately.
#    a. Exec into container:  docker exec -it debian-desktop /bin/bash
#    b. Remove old passwd:   rm -f /home/debian/.vnc/passwd
#    c. Set new password:    vncpasswd
#    d. Exit terminal:       exit
#    e. Restart container:   docker restart debian-desktop
#
# Access VNC at: http://localhost:6080
# --------------------------------------------------------------------------------------------------
