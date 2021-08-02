# UbuntuDocker
Docker Ubuntu18-Opencv4.2


in Raspberry Pi4 (armV7l_32bit) os use Docker .
this project for job use so if Encounter difficulties issue you can Ask 

#Remark 
the environment total  about 1.5GB .
Mainly use python3 、Opencv、Python3-dev、Python-numpy



#Supply Raspberry Pi image the Dockerfile didn't havd CMD["/bin/bash"] you should add "/bin/bash" in the docker build .

FROM balenalib/raspberry-pi-node


RUN install_packages python3 && apt-get update -y && apt-get upgrade -y && apt-get install -y apt-utils 
RUN apt install build-essential cmake git pkg-config libgtk-3-dev \
    libavcodec-dev libavformat-dev libswscale-dev libv4l-dev \
    libxvidcore-dev libx264-dev libjpeg-dev libpng-dev libtiff-dev \
    gfortran openexr libatlas-base-dev python3-dev python3-numpy \
    wget unzip net-tools libtbb2 libtbb-dev libdc1394-22-dev -y
	
	
RUN mkdir ~/opencv_build && cd ~/opencv_build && \
	wget -O opencv.zip https://github.com/opencv/opencv/archive/3.4.3.zip && \
	wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/3.4.3.zip && \
	unzip opencv.zip && unzip opencv_contrib.zip && rm -r -f opencv.zip && rm -r -f opencv_contrib.zip && cd ~/opencv_build/opencv-3.4.3 && mkdir build && cd build && \
	cmake -D CMAKE_BUILD_TYPE=RELEASE \
    		-D CMAKE_INSTALL_PREFIX=/usr/local \
   		 -D INSTALL_C_EXAMPLES=ON \
   		 -D INSTALL_PYTHON_EXAMPLES=ON \
   		 -D OPENCV_GENERATE_PKGCONFIG=ON \
   		 -D OPENCV_EXTRA_MODULES_PATH=~/opencv_build/opencv_contrib-3.4.3/modules \
   		 -D BUILD_EXAMPLES=ON ..\
	&&\
	make -j4 && make install
