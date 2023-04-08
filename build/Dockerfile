FROM golang:1.19.7-alpine3.17 AS builder

WORKDIR /build

#ENV CGO_ENABLED 0
#ENV GOOS linux
#ENV GOPROXY https://goproxy.cn,direct

COPY go.mod .
COPY go.sum .
RUN go mod download
COPY . .

RUN go build -ldflags="-s -w" -o cmd/server cmd/server.go

CMD ["./server"]

FROM alpine

WORKDIR /build

ENV TZ Asia/Shanghai

COPY --from=builder /build/cmd/server .

EXPOSE 8080

CMD ["./server"]