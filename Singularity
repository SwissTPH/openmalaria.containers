####################################
# Singularity recipe for openMalaria version 38
#
####################################

Bootstrap: docker
From: centos:7

%post

   export OPENMALARIA_VERSION="38.0"

   # install the OpenMalaria dependencies
   yum -y install epel-release
   yum -y install \
   boost-devel \
   cmake \
   gcc-c++ \
   glibc-devel \
   gsl-devel \
   make \
   wget \
   xerces-c-devel \
   xsd \
   zlib-devel
   yum clean all

   # download the source code and compile it
   cd /usr/local/src/
   wget https://github.com/SwissTPH/openmalaria/archive/schema-${OPENMALARIA_VERSION}.tar.gz
   tar xf schema-${OPENMALARIA_VERSION}.tar.gz
   mkdir -p /usr/local/src/openmalaria-schema-${OPENMALARIA_VERSION}/build/
   cd /usr/local/src/openmalaria-schema-${OPENMALARIA_VERSION}/build/
   cmake .. -DCMAKE_BUILD_TYPE=RELEASE
   make

   # copy the binary and resource files to the bin/ folder
   cp openMalaria /usr/local/bin
   cp schema/scenario_current.xsd /usr/local/bin/
   cp ../test/densities.csv /usr/local/bin/


%runscript
   exec openMalaria "$@"

%apprun openmalaria
openMalaria "@"i

%help
To see the openMalaria command help, use the -h option
