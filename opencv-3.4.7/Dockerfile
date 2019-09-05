FROM ubuntu:bionic

# install opencv dependencies
RUN apt-get update
RUN apt-get install -y build-essential cmake wget unzip pkg-config \
    libjpeg-dev libpng-dev libtiff-dev \
    libavcodec-dev libavformat-dev libswscale-dev libv4l-dev \ 
    libxvidcore-dev libx264-dev \
    libgtk-3-dev \
    libatlas-base-dev gfortran \
    python3-dev

RUN apt-get -y install python3-pip
RUN pip3 install numpy

# get opencv source
WORKDIR /opencv
RUN wget -O opencv.zip https://github.com/opencv/opencv/archive/3.4.7.zip
RUN wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/3.4.7.zip
RUN unzip opencv.zip && unzip opencv_contrib.zip
RUN mv opencv-3.4.7 opencv && mv opencv_contrib-3.4.7 opencv_contrib

# compile & install opencv
WORKDIR /opencv/opencv
RUN mkdir build
WORKDIR /opencv/opencv/build
RUN cmake -D CMAKE_BUILD_TYPE=RELEASE \
	-D CMAKE_INSTALL_PREFIX=/usr/local \
    -D INSTALL_PYTHON_EXAMPLES=ON \
	-D INSTALL_C_EXAMPLES=ON \
	-D OPENCV_ENABLE_NONFREE=ON \
	-D OPENCV_EXTRA_MODULES_PATH=/opencv/opencv_contrib/modules \
    -D PYTHON_EXECUTABLE=/usr/bin/python3.6 \
	-D BUILD_EXAMPLES=ON ..
RUN make -j8 && make install && ldconfig

CMD [ "/bin/bash" ]