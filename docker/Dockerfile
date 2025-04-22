FROM golang:1.20.7 AS builder
LABEL maintainer="dharitri"

RUN apt-get update && apt-get install -y

WORKDIR /config
COPY . .

WORKDIR /go
RUN git clone https://github.com/TerraDharitri/drt-go-chain.git && cd drt-go-chain && git checkout main
#--force $(cat /config/binaryVersion)
WORKDIR /go/drt-go-chain

#Dharitri node
WORKDIR /go/drt-go-chain/cmd/node
# RUN go build -v -ldflags="-X main.appVersion=$(git --git-dir /config/.git describe --tags --long --dirty)"
RUN go build 


RUN mkdir -p /lib_amd64 /lib_arm64


RUN cp /go/pkg/mod/github.com/!terra!dharitri/$(cat /go/drt-go-chain/go.mod | grep drt-go-chain-vm-v2 | sort -n | tail -n -1| awk -F '/' '{print$3}'| sed 's/ /@/g')/wasmer/libwasmer_linux_amd64.so /lib_amd64/
# RUN cp /go/pkg/mod/github.com/!terra!dharitri/$(cat /go/drt-go-chain/go.mod | grep -w 'drt-go-chain-vm' | sort -n | tail -n -1| awk -F '/' '{print$3}'| sed 's/ /@/g')/wasmer2/libvmexeccapi.so /lib_amd64/
RUN cp /go/pkg/mod/github.com/!terra!dharitri/drt-go-chain-vm@v0.0.4/wasmer2/libvmexeccapi.so /lib_amd64/



RUN cp /go/pkg/mod/github.com/!terra!dharitri/$(cat /go/drt-go-chain/go.mod | grep drt-go-chain-vm-v2 | sort -n | tail -n -1 | awk -F '/' '{print$3}' | sed 's/ /@/g')/wasmer/libwasmer_linux_arm64_shim.so /lib_arm64/
# RUN cp /go/pkg/mod/github.com/!terra!dharitri/$(cat /go/drt-go-chain/go.mod | grep -w 'drt-go-chain-vm' | sort -n | tail -n -1 | awk -F '/' '{print$3}' | sed 's/ /@/g')/wasmer2/libvmexeccapi_arm.so /lib_arm64/
RUN cp /go/pkg/mod/github.com/!terra!dharitri/drt-go-chain-vm@v0.0.4/wasmer2/libvmexeccapi_arm.so /lib_arm64/



WORKDIR /config
RUN cp -r * /go/drt-go-chain/cmd/node/config/

WORKDIR /go/drt-go-chain/cmd/node

# ===== SECOND STAGE ======
FROM ubuntu:22.04
ARG TARGETARCH
RUN apt-get update -y && apt-get upgrade -y

# COPY --from=builder "/go/drt-go-chain/cmd/node" "/go/drt-go-chain/cmd/node/"
COPY --from=builder "/go/drt-go-chain/cmd/node/." "/go/drt-go-chain/cmd/node/"


# Copy architecture-specific files
COPY --from=builder "/lib_${TARGETARCH}/*" "/lib/"

WORKDIR /go/drt-go-chain/cmd/node/
EXPOSE 8200
ENTRYPOINT ["/go/drt-go-chain/cmd/node/node", "--rest-api-interface=:8200"]
