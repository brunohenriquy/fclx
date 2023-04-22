FROM golang:1.20.3

# Set environment variables
ENV PATH="/root/.cargo/bin:${PATH}"
ENV USER=root

# Install Rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y \ 
    && rustup default stable \ 
    && rustup target add x86_64-unknown-linux-gnu

WORKDIR /go/src
RUN ln -sf /bin/bash /bin/sh
COPY go.mod go.sum ./
RUN go mod download && go mod verify
COPY . .

RUN cd /go/pkg/mod/github.com/j178/tiktoken-go@v0.2.1/tiktoken-cffi && \
    cargo build --release

RUN apt update && apt install -y protobuf-compiler=3.12.4-1 && apt install -y protoc-gen-go=1.25.0+git20201208.160c747-1+b5
RUN go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.2 && go install github.com/kyleconroy/sqlc/cmd/sqlc@v1.17.2

#RUN curl -L https://github.com/golang-migrate/migrate/releases/download/v4.15.2/migrate.linux-arm64.tar.gz | tar xvz

CMD [ "tail", "-f", "/dev/null" ]