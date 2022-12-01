# NovemberCreation: Developing a light-weight Digital Forensics environment for investigative use.
Brian Busco, Ethan Thach, Kaden Makechnie-Hardy, Justin Mott, Quincy Taylor, Braden Muns

## Outline
Comparison to SIFT

Why each application?

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
