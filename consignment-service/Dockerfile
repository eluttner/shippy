FROM golang:1.10.2 as builder

WORKDIR /go/src/github.com/eluttner/shippy/consignment-service

COPY . .

ENV GIT_TERMINAL_PROMPT=1

RUN go get -u github.com/golang/dep/cmd/dep
RUN dep init 
RUN GIT_TERMINAL_PROMPT=1 dep ensure
#RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo .
RUN CGO_ENABLED=0 GOOS=linux go build  -o consignment-service -a -installsuffix cgo main.go repository.go handler.go datastore.go


FROM alpine:latest

RUN apk --no-cache add ca-certificates

RUN mkdir /app
WORKDIR /app
COPY --from=builder /go/src/github.com/eluttner/shippy/consignment-service/consignment-service .

CMD ["./consignment-service"]