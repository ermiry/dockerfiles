FROM ubuntu:bionic

RUN apt-get update && apt-get install -y build-essential cmake wget

WORKDIR /app
RUN wget https://github.com/mongodb/mongo-c-driver/releases/download/1.15.1/mongo-c-driver-1.15.1.tar.gz
RUN tar xzf mongo-c-driver-1.15.1.tar.gz

WORKDIR /app/mongo-c-driver-1.15.1/cmake-build
RUN cmake -DENABLE_AUTOMATIC_INIT_AND_CLEANUP=OFF -DCMAKE_BUILD_TYPE=Release ..
RUN make -j4 && make install

CMD ["/bin/bash"]