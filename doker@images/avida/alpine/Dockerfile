FROM ubuntu:20.04 as avida-builder
ARG DEBIAN_FRONTEND=noninteractive
WORKDIR /gitlab.com/fortunalab/
RUN apt-get update  && apt-get -y --no-install-recommends install \
    ca-certificates \
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
RUN git submodule update --init --recursive
RUN ./build_avida

FROM alpine:3.15.4
RUN set -x && \
  apk add --no-cache --update \
    libstdc++ \
    gcompat
WORKDIR /avida/
COPY --from=avida-builder /gitlab.com/fortunalab/avida/cbuild/work/ .
