# NovemberCreation: Developing a light-weight Digital Forensics environment for investigative use.
Brian Busco, Ethan Thach, Kaden Makechnie-Hardy, Justin Mott, Quincy Taylor

## Outline

## Files

## Instructions for Use

STEP 1: 

Download the Dockerfile to your working directory.

<img width="682" alt="image" src="https://user-images.githubusercontent.com/67716541/204440009-38101024-e02c-41fb-bf01-0cbfaa7fc0dd.png">

STEP 2:

Build the new container image with this command:

` docker build -t november-creation .`

After the build, you should see this:

<img width="682" alt="image" src="https://user-images.githubusercontent.com/67716541/204440745-f2826868-c0ca-4e69-a5a4-e480d862f0fe.png">

STEP 3:

Now, run this command to start a real container based on the image you just built. The -it is important because that lets you tty into the container.

`docker run -it -d november-creation`

You should see this when you run the command:

<img width="682" alt="image" src="https://user-images.githubusercontent.com/67716541/204442672-2b00c7f8-b6ea-41ea-ae8f-c933f2789522.png">

STEP 4:

To access your machine, go to docker desktop and find your running container. You may access the terminal and run commands in the container here:

<img width="1290" alt="image" src="https://user-images.githubusercontent.com/67716541/204442969-fa5f495a-a28c-47af-9ac9-7a7270cd4e7b.png">

Or you may more directly access the machine by copying the output from `run` and loading it into this command:

`docker exec -it <your output here> /bin/sh`

This option looks like this:

<img width="983" alt="image" src="https://user-images.githubusercontent.com/67716541/204443366-1ba4519d-8a12-4714-96cc-49ec9ed59645.png">


## Test Cases
