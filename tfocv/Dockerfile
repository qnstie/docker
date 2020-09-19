FROM nvcr.io/nvidia/tensorflow:19.01-py3
LABEL maintainer "Pawel Kunstman <pawel@kunstman.net>"

#OCV build taken from: https://github.com/janza/docker-python3-opencv/blob/master/Dockerfile


RUN apt-get update && apt-get install -y \
	mc \
	python3-tk \
	graphviz \
	build-essential \
        cmake \
        git \
        wget \
        unzip \
        yasm \
        pkg-config \
        libswscale-dev \
        libtbb2 \
        libtbb-dev \
        libjpeg-dev \
        libpng-dev \
        libtiff-dev \
        libavformat-dev \
        libpq-dev \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

RUN pip install --upgrade pip

RUN pip install pydot graphviz imageio scikit-image numpy

WORKDIR /
ENV OPENCV_VERSION="3.4.5"
RUN wget https://github.com/opencv/opencv_contrib/archive/${OPENCV_VERSION}.zip \
&& unzip ${OPENCV_VERSION}.zip \
&& rm ${OPENCV_VERSION}.zip
RUN wget https://github.com/opencv/opencv/archive/${OPENCV_VERSION}.zip \
&& unzip ${OPENCV_VERSION}.zip \
&& mkdir /opencv-${OPENCV_VERSION}/cmake_binary \
&& cd /opencv-${OPENCV_VERSION}/cmake_binary \
&& cmake -DBUILD_TIFF=ON \
  -DBUILD_opencv_java=OFF \
  -DOPENCV_EXTRA_MODULES_PATH=/opencv_contrib-${OPENCV_VERSION}/modules \
  -DWITH_CUDA=OFF \
  -DWITH_OPENGL=ON \
  -DWITH_OPENCL=ON \
  -DWITH_IPP=ON \
  -DWITH_TBB=ON \
  -DWITH_EIGEN=ON \
  -DWITH_V4L=ON \
  -DBUILD_TESTS=OFF \
  -DBUILD_PERF_TESTS=OFF \
  -DCMAKE_BUILD_TYPE=RELEASE \
  -DINSTALL_C_EXAMPLES=OFF \
  -DINSTALL_PYTHON_EXAMPLES=OFF \
  -DBUILD_EXAMPLES=OFF \
#  -DWITH_CUDA=ON \
  -DCMAKE_INSTALL_PREFIX=$(python3 -c "import sys; print(sys.prefix)") \
  -DPYTHON_EXECUTABLE=$(which python3) \
  -DPYTHON_INCLUDE_DIR=$(python3 -c "from distutils.sysconfig import get_python_inc; print(get_python_inc())") \
  -DPYTHON_PACKAGES_PATH=$(python3 -c "from distutils.sysconfig import get_python_lib; print(get_python_lib())") \
  .. \
&& make install \
&& rm /${OPENCV_VERSION}.zip \
&& rm -r /opencv-${OPENCV_VERSION}


#RUN ln -s \
#  /usr/lib/python3.5/dist-packages/cv2/python-3.5/cv2.cpython-35m-x86_64-linux-gnu.so \
#  /usr/local/lib/python3.5/dist-packages/cv2.so

ENTRYPOINT []
CMD ["/bin/bash"]
