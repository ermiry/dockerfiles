## OpenCV 3.4.7

**Base:** ubuntu:bionic

Installs OpenCV dependencies, downloads OpenCV 3.4.7 source from official repo, compiles using -j8 flag (you can change it to the number of processors you have), and finally it installs OpenCV.

## Usage:

`sudo docker build -t ermiry/ubuntu-opencv:3.4.7 .`