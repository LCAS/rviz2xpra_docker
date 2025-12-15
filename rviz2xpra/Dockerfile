# ###########################################################################
# Dockerfile for XPRA + RViz2 Browser Display
#
# Container image combining XPRA HTML5 server with ROS2 RViz for browser-based
# visualization of ROS topics and transforms.
#
# @author      James R. Heselden (github: iranaphor)
# @maintainer  James R. Heselden (github: iranaphor)
# @datecreated 30th November 2025
# @credits     Code structure and implementation were developed by the
#              author with assistance from Anthropic's Claude Sonnet 4.5
#              model via GitHub Copilot, used under the author's direction
#              and supervision.
#
###########################################################################

FROM ros:humble

# Installl rviz2
RUN apt-get update && \ 
    apt-get install -y \
    ros-humble-rviz2 \
    && rm -rf /var/lib/apt/lists/*

# Install XPRA and dependencies
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get install -y \
    xpra \
    xvfb \
    websockify \
    python3-rencode \
    && rm -rf /var/lib/apt/lists/*

# Copy startup script
COPY start.sh /start.sh
RUN chmod +x /start.sh

# Expose XPRA HTML5 port
EXPOSE 14500

# Set working directory
WORKDIR /root

CMD ["/start.sh"]
