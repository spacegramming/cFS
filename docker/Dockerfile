FROM ubuntu:18.04
MAINTAINER Karsten Gordon <karsten.gordon@spacegramming.com>

# Install toolchain to build cFS
RUN apt-get update \
    && apt-get -y install git cmake doxygen

# Install toolchain to build and run ground station
RUN apt-get update \
    && apt-get -y install python3-pyqt5 python3-zmq libcanberra-gtk-module

# Install additional display drivers
RUN apt-get update \
    && apt-get -y install mesa-utils and libgl1-mesa-glx

# Copy the current repo content into the container 
# to the local changes
COPY . /cFS

# Build the groud system software
WORKDIR /cFS/tools/cFS-GroundSystem/Subsystems/cmdUtil
RUN make

# Build the mission software
WORKDIR /cFS
RUN cp cfe/cmake/Makefile.sample Makefile
RUN cp -r cfe/cmake/sample_defs sample_defs
RUN make SIMULATION=native prep
RUN make
RUN make install

# Run the groud system software
WORKDIR /cFS/tools/cFS-GroundSystem
#CMD ["python3", "GroundSystem.py"]

# Run the mission software
#WORKDIR /cFS/build/exe/cpu1
#CMD ["./core-cpu1"]
