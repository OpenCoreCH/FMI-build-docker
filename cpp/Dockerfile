FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y cmake build-essential curl libcurl4-openssl-dev openssl libssl-dev git zlib1g zlib1g-dev
RUN git clone --recurse-submodules https://github.com/aws/aws-sdk-cpp.git && cd aws-sdk-cpp && mkdir build && cd build && \
    cmake -DCMAKE_BUILD_TYPE=Release -DBUILD_ONLY="s3" -DBUILD_SHARED_LIBS="off" .. && make -j6 install && cd ../.. && rm -rf aws-sdk-cpp
RUN curl -LO https://boostorg.jfrog.io/artifactory/main/release/1.77.0/source/boost_1_77_0.tar.gz && tar -xvf boost_1_77_0.tar.gz && \
    cd boost_1_77_0 && ./bootstrap.sh && ./b2 cxxflags="-fPIC" link=static install && cd .. && rm -rf boost*
RUN git clone https://github.com/redis/hiredis.git && cd hiredis/ && make install && cd .. && rm -rf hiredis
