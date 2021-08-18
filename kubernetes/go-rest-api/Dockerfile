FROM golang:1.17.0-alpine3.14 as builder
COPY go.mod go.sum  /go/src/github.com/jonarosero/go-rest-api/
WORKDIR /go/src/github.com/jonarosero/go-rest-api/
RUN go mod download
COPY . /go/src/github.com/jonarosero/go-rest-api/
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o build/go-rest-api github.com/jonarosero/go-rest-api/

FROM alpine
RUN apk add --no-cache ca-certificates && update-ca-certificates
COPY --from=builder /go/src/github.com/jonarosero/go-rest-api/ /usr/bin/go-rest-api
EXPOSE 8080 8080
ENTRYPOINT ["/usr/bin/go-rest-api"]