FROM gcc as builder

RUN apt-get update && apt-get install -y cmake
# RUN apt-get install -y libssl-dev

RUN wget https://github.com/mongodb/mongo-c-driver/releases/download/1.15.1/mongo-c-driver-1.15.1.tar.gz
RUN tar xzf mongo-c-driver-1.15.1.tar.gz

WORKDIR mongo-c-driver-1.15.1/cmake-build
RUN cmake -D ENABLE_AUTOMATIC_INIT_AND_CLEANUP=OFF -D CMAKE_BUILD_TYPE=Release -D ENABLE_SSL=OPENSSL ..
RUN make -j4 && make install

# copy your own code here to be compilled
# WORKDIR /
# COPY . .
# RUN make -j4

############
FROM ubuntu
RUN apt-get update && apt-get install -y libssl-dev && apt-get clean

COPY --from=builder /usr/lib/x86_64-linux-gnu/libicudata.so.63 /usr/lib/x86_64-linux-gnu/libicudata.so.63
COPY --from=builder /usr/lib/x86_64-linux-gnu/libicuuc.so.63 /usr/lib/x86_64-linux-gnu/libicuuc.so.63
COPY --from=builder /usr/local/include/ /usr/local/include/
COPY --from=builder /usr/local/lib/libmongoc-1.0.so /usr/local/lib/libmongoc-1.0.so
COPY --from=builder /usr/local/lib/libbson-1.0.so /usr/local/lib/libbson-1.0.so

RUN ldconfig

# copy you executable & set its as the entry point
# WORKDIR /home/
# COPY --from=builder ./bin/cerver .
# CMD ["./cerver"]