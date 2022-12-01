#Download base image ubuntu 20.04
FROM ubuntu:20.04

# LABEL about the custom image
LABEL maintainer="Group 1"
LABEL version="0.1"
LABEL description="This is custom Docker Image for \
the PHP-FPM and Nginx Services."

# Disable Prompt During Packages Installation
ARG DEBIAN_FRONTEND=noninteractive

# Update Ubuntu Software repository
RUN apt update && \

# Install Nmap tool
apt install nmap -y && \

# Install Tshark
apt install -y tshark && \

#Install TCPdump
apt install -y tcpdump && \

# Install Sleuth Kit
apt install sleuthkit -y && \

# Output versions
echo "--------------------------" >> ToolVersions.txt && \
nmap --version >> ToolVersions.txt && \

echo "--------------------------" >> ToolVersions.txt && \
tshark --version >> ToolVersions.txt && \

echo "--------------------------" >> ToolVersions.txt && \
fls -V >> ToolVersions.txt

CMD tcpdump --version >> ToolVersions.txt && \
cat ToolVersions.txt && \
tail -f /dev/null