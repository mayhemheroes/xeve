# Build Stage:
FROM --platform=linux/amd64 ubuntu:20.04 as builder

## Install build dependencies.
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y gcc make cmake build-essential

## Add Source Code
ADD / /xeve-mayhem
WORKDIR /xeve-mayhem


## Build Step 
RUN mkdir build \
   && cd build \
   && cmake .. -DSET_PROF=BASE \
   && make \
   && make install
   

# Package Stage
FROM --platform=linux/amd64 ubuntu:20.04
COPY --from=builder /xeve-mayhem/build/bin/. /
COPY --from=builder /xeve-mayhem/build/lib/. /lib
COPY --from=builder /xeve-mayhem/testsuite /testsuite

# Instructions to get the built libraries into a common place to have the executable load them
# RUN cd ~ \
#    && cp -a /lib/wjelement/. /lib/ \
#    && cp -a /lib/wjwriter/. /lib/ \
#    && cp -a /lib/wjreader/. /lib/ \
#    && cp -a /lib/lib/. /lib/