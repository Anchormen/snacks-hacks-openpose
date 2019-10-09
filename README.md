# Introduction
This is the companion repo for our 5th Snacks & Hacks meetup

# How to build

The following command will build an image with the tag snacks-hacks-openpose:latest. There are 2 flavors, CPU or GPU (Cuda10):

`docker build -t snacks-hacks-openpose:latest https://raw.githubusercontent.com/Anchormen/snacks-hacks-openpose/{BRANCH}/Dockerfile.cpu`

or for GPU:

`docker build -t snacks-hacks-openpose:latest https://raw.githubusercontent.com/Anchormen/snacks-hacks-openpose/{BRANCH}/Dockerfile.cuda10_1.gpu`

# How to run

From your host system run the following to add all users to X:

`xhost local:` or `xhost +`

Run the following command for starting the image build under the snacks-hacks-openpose:latest, the CPU version requires the repository to be mounted as a volume under /opt/anchormen

`docker run -v /tmp/.X11-unix:/tmp/.X11-unix -v /dev/snd:/dev/snd -v ${REPO_PATH}/snacks-hacks-openpose:/opt/anchormen -e DISPLAY=$DISPLAY --device=/dev/video0:/dev/video0 -it snacks-hacks-openpose:latest`

or for GPU:

`docker run --runtime=nvidia --ipc=host -v /tmp/.X11-unix:/tmp/.X11-unix -v /dev/snd:/dev/snd  -e DISPLAY=$DISPLAY --device=/dev/video0:/dev/video0 -it snacks-hacks-openpose:latest`

The following part: `/tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY`, is for mapping the display from docker to the host screen.

Now you should be in the container's shell.

Start the demo:

`python3 demo.py`

