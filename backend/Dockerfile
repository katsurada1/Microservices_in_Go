FROM golang:1.20rc1

ENV GOPATH /go/src

RUN mkdir /go/src/backend
WORKDIR /go/src/backend

COPY go.mod /go/src/backend/go.mod
COPY go.sum /go/src/backend/go.sum

RUN go mod download

