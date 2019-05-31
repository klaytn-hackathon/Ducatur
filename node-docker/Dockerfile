FROM ubuntu:18.04

# update ubuntu & install wget
RUN apt-get update
RUN apt-get install -y wget tar

WORKDIR /root/

# just for fun
RUN mkdir ~/klaytn

# download and install klaytn endpoint node
RUN wget http://packages.klaytn.net/klaytn/v0.8.2/ken-v0.8.2-30-linux-amd64.tar.gz
RUN tar zxf ken-v0.8.2-30-linux-amd64.tar.gz
RUN export PATH=$PATH:$PWD/ken-linux-amd64/bin

# TODO: move this to initial install (not doing it now for network efficency reasons)
RUN apt-get install -y curl

# configure klaytn endpoint node
RUN mkdir -p ~/kend_home
RUN curl -X GET http://packages.klaytn.net/baobab/genesis.json -o genesis.json

RUN apt-get install -y libleveldb-dev
# RUN apt-get install -y libsnappy-dev make
# RUN wget https://github.com/google/leveldb/archive/1.22.tar.gz
# # RUN wget https://leveldb.googlecode.com/files/leveldb-1.9.0.tar.gz
# RUN tar -xzf 1.22.tar.gz
# RUN cd leveldb-1.22
# RUN make
# RUN mv libleveldb.* /usr/local/lib
# RUN cd include
# RUN cp -R leveldb /usr/local/include
# RUN ldconfig

# start 
# CMD [ "ken", "init", "--datadir ~/kend_home", "genesis.json" ]
# ENTRYPOINT [ "sh", "-c", "./ken-linux-amd64/bin/ken init --datadir ~/kend_home genesis.json"]
RUN ./ken-linux-amd64/bin/ken init --datadir ~/kend_home genesis.json

COPY kend.conf ./ken-linux-amd64/conf/kend.conf
# RUN cat ~/ken-linux-amd64/conf/kend.conf
COPY entrypoint.sh ./entrypoint.sh
RUN chmod +x entrypoint.sh

EXPOSE 8551 8552 32323 32323/udp 32324 32324/udp

# ENTRYPOINT [ "sh", "-c", "cat ~/ken-linux-amd64/conf/kend.conf" ]
ENTRYPOINT [ "sh", "-c", "./entrypoint.sh" ]
# CMD [ "sh", "-c", "./ken-linux-amd64/bin/kend start"]
