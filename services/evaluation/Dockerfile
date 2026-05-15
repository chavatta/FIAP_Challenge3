# syntax=docker/dockerfile:1
FROM golang:1.22-alpine AS build
WORKDIR /src
COPY go.mod ./
COPY *.go ./
RUN go mod tidy && CGO_ENABLED=0 go build -o /out/app .

FROM alpine:3.19
RUN adduser -D -u 65532 appuser
USER appuser
COPY --from=build /out/app /app
ENTRYPOINT ["/app"]
