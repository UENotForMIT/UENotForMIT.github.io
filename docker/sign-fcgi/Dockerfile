# syntax=docker/dockerfile:1

## Build
FROM  golang:1.16-alpine as build

WORKDIR   /app

COPY  go.mod  ./
COPY go.sum ./
RUN  go mod download

COPY   *.go ./

RUN go build -o /sign_binary

## Deploy
FROM gcr.io/distroless/base-debian11

WORKDIR /

COPY --from=build  /sign_binary /sign_binary

EXPOSE 7352

USER nonroot:nonroot

ENTRYPOINT ["/sign_binary"]