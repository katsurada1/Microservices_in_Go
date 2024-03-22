FROM golang:1.20rc1

ENV GOPATH /go/src

RUN mkdir /go/src/frontend
WORKDIR /go/src/frontend

COPY go.mod /go/src/frontend/go.mod
# COPY go.sum /go/src/frontend/go.sum

RUN go mod download

