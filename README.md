# NovemberCreation: Developing a Light-Weight Digital Forensics and Incident Response Environment for Investigative Use.
Brian Busco, Ethan Thach, Kaden Makechnie-Hardy, Justin Mott, Quincy Taylor, Braden Muns

## Outline
Comparison to SIFT

In 2007 a researcher at SANs created the SIFT Workstation to aid in digital forensic investigations by providing the necessary tooling in a single location. The SIFT workstation is a collection of open-source IR and forensic tools designed to perform investigations including tools for packet inspection and file system analysis.

Similar to the SIFT workstation developed by SANs, this Docker configuration provides common tooling for digital forensics investigations. While the SIFT Workstation contains tools for analyzing file systems, network evidence, and memory images, our November Creation focuses on network and file system forensics. A list of the applications included in the configurations and the justification for their inclusion is included below.
### nmap
Nmap is a light-weight command line tool for network scanning and mapping. Nmap allows users to detect hosts and services on a network by sending packets and analyzing the responses. A key digital forensics principle is to know your assets. It is crucial for organizations to inventory enterprise networks.
### TShark
TShark is a command line tool that can capture and inspect packets. Information about network traffic can provide crucial information during a forensics investigation. TShark is valuable because it has similar capabilities to the Wireshark GUI including the ability to detect, inspect, and write to the the same file types providing flexibility during the investigation.
### tcpdump
tcpdump provides the ability to create and analyze packet captures of network traffic. It is a packet sniffing and packet analyzing tool which allows for filtering for greater security insights. tcpdump can offer greater flexibility than TShark for investigative work.
### The Sleuth Kit
The Sleuth Kit is a file system analysis tool that allows the investigator to extract data from drives and storage for closer analysis. The Sleuth Kit is a command line version of Autopsy and provides similar functionalities.

## Files

### Docker Config File
```
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
```

## Instructions for Use

STEP 1: 

Download the Dockerfile to your working directory.

<img width="1290" alt="image" src="https://user-images.githubusercontent.com/67716541/204440009-38101024-e02c-41fb-bf01-0cbfaa7fc0dd.png">

STEP 2:

Build the new container image with this command:

` docker build -t november-creation .`

After the build, you should see this:

<img width="1290" alt="image" src="https://user-images.githubusercontent.com/67716541/204440745-f2826868-c0ca-4e69-a5a4-e480d862f0fe.png">

STEP 3:

Now, run this command to start a real container based on the image you just built. The -it is important because that lets you tty into the container.

`docker run -it -d november-creation`

You should see this when you run the command:

<img width="1290" alt="image" src="https://user-images.githubusercontent.com/67716541/204442672-2b00c7f8-b6ea-41ea-ae8f-c933f2789522.png">

STEP 4:

To access your machine, go to docker desktop and find your running container. You may access the terminal and run commands in the container here:

<img width="1290" alt="image" src="https://user-images.githubusercontent.com/67716541/204442969-fa5f495a-a28c-47af-9ac9-7a7270cd4e7b.png">

Or you may more directly access the machine by copying the output from `run` and loading it into this command:

`docker exec -it <your output here> /bin/sh`

This option looks like this:

<img width="1290" alt="image" src="https://user-images.githubusercontent.com/67716541/204443366-1ba4519d-8a12-4714-96cc-49ec9ed59645.png">


## Test Cases
On configuration of the image, a log of the tools and corresponding version information is stored in ToolVersions.txt within the root directory. When a container is launched, ToolVersions.txt is outputted to the screen and the container is run in detached mode to keep the workstation open. The correct version information included in the ToolVersions.txt file demonstrates that the applications have been correctly installed and can be utilized by users of the light-weight digital forensics environment.

Example version output on launch of container:

<img width="1290" alt="image" src="https://user-images.githubusercontent.com/28959765/204937333-e17e304d-fe44-473f-9a97-e1d9c0918626.png">
