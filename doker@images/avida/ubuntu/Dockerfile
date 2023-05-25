FROM ubuntu:20.04 as avida-build
ARG DEBIAN_FRONTEND=noninteractive
WORKDIR /gitlab.com/fortunalab/
RUN apt-get update  && apt-get install -y \
    gcc-9 \
    g++-9 \
    cmake \
    make \
    git \
    curl \
&& update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 100 \
&& update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 100 \ 
&& git clone https://gitlab.com/fortunalab/avida.git
WORKDIR /gitlab.com/fortunalab/avida
RUN git submodule foreach git fetch
RUN git submodule update
RUN git submodule init
RUN ./build_avida

FROM ubuntu:20.04
WORKDIR /avida/
COPY --from=avida-build /gitlab.com/fortunalab/avida/cbuild/work/ .
