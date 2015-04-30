
FROM ubuntu:14.10

MAINTAINER Mirco Zeiss <mirco.zeiss@gmail.com>

# update repository
# https://github.com/golang/go/wiki/InstallFromSource#install-c-tools
RUN \
  apt-get update && \
  apt-get install -y \
    gcc \
    libc6-dev \
    git

# install go
WORKDIR /usr/src
RUN git clone https://go.googlesource.com/go
WORKDIR ./go
RUN git checkout go1.4.1

WORKDIR ./src
RUN ./all.bash

# set paths
ENV PATH /usr/src/go/bin:$PATH

RUN mkdir -p /go/src/github.com/zemirco/app
ENV GOPATH /go
ENV PATH /go/bin:$PATH

# check installation
RUN go version

# add go app
ADD app.go /go/src/github.com/zemirco/app/app.go

# Build the app command inside the container
# (You may fetch or manage dependencies here,
# either manually or with a tool like "godep".)
WORKDIR /go/src/github.com/zemirco/app
RUN go install

# Run the outyet command by default when the container starts
ENTRYPOINT /go/bin/app

# Document that the service listens on port 8080
EXPOSE 8080
