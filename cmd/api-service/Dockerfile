FROM golang:1.22-alpine AS builder
WORKDIR /src

COPY go.mod ./
RUN go mod download

COPY cmd ./cmd

RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -trimpath -ldflags="-s -w" -o /out/api-service ./cmd/api-service

FROM alpine:3.20
WORKDIR /app
COPY --from=builder /out/api-service /app/api-service
EXPOSE 8080
ENTRYPOINT ["/app/api-service"]
