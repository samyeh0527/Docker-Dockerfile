
#base image
FROM balenalib/raspberry-pi-node
#install pkg
RUN install_packages python3 && apt-get update -y && apt-get upgrade -y && apt-get install -y apt-utils && \
    apt install build-essential cmake git pkg-config libgtk-3-dev \
    libavcodec-dev libavformat-dev libswscale-dev libv4l-dev \
    libxvidcore-dev libx264-dev libjpeg-dev libpng-dev libtiff-dev \
    gfortran openexr libatlas-base-dev python3-dev python3-numpy \
    wget unzip net-tools libtbb2 libtbb-dev libdc1394-22-dev libusb-1.0-0-dev -y
	
#create opencv file and use cmake build env  ... finlly will delete opencv_contrib	
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
    		 -D BUILD_EXAMPLES=ON .. \
 	&& \
 	make -j4 && make install \
	&& cd && rm -f -r opencv_build 
	
#download script for autoRun and uninstall unzip wget  
#add 720 rules 
RUN  mkdir Desktop && cd /Desktop && wget -O 100_ToTaipei.zip https://raw.githubusercontent.com/samyeh0527/Docker-Dockerfile/main/100_ToTaipei.zip && \
 	unzip 100_ToTaipei.zip && rm -r -f 100_ToTaipei.zip &&  cd 100_ToTaipei/host_lib &&  mkdir build && cd build && \ 
  	cmake ..  &&  make -j2   && apt-get remove unzip wget && \ 
	echo "KERNEL=="ttyUSB*",ATTRS{idVendor}=="067b",ATTRS{idProduct}=="2303",MODE="0777",SYMLINK+="kneron_uart" " >> /etc/udev/rules.d/10-local.rules   && \
	echo "KERNEL=="ttyUSB*",ATTRS{idVendor}=="1a86",ATTRS{idProduct}=="7523",MODE="0777",SYMLINK+="kneron_pwr" " >> /etc/udev/rules.d/10-local.rules	&& \
	echo "SUBSYSTEM=="usb",ATTRS{idVendor}=="3231",ATTRS{idProduct}=="0200",MODE="0666”" >> /etc/udev/rules.d/10-local.rules

	
	

WORKDIR /Desktop/100_ToTaipei
CMD ["/bin/bash","./autoRun.sh"]
VOLUME /Desktop
