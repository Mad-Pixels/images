ARG ALPINE_VERSION=3.20

# build image ->
FROM --platform=$BUILDPLATFORM alpine:${ALPINE_VERSION} AS builder
RUN apk add --no-cache go git

ENV GOPATH=/go \
    GOCACHE=/tmp/.cache \
    PATH=/go/bin:/usr/local/go/bin:$PATH
RUN go install github.com/rhysd/actionlint/cmd/actionlint@latest

# final image ->
FROM --platform=$TARGETPLATFORM scratch
COPY --from=builder /go/bin/actionlint /actionlint
ENTRYPOINT ["/actionlint"]

