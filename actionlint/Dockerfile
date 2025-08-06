ARG ALPINE_VERSION

# build image ->
FROM --platform=$BUILDPLATFORM alpine:${ALPINE_VERSION} AS builder
ARG ACTIONLINT_VER

RUN apk add --no-cache go=latest git=latest
ENV GOPATH=/go \
    GOCACHE=/tmp/.cache \
    PATH=/go/bin:/usr/local/go/bin:$PATH
RUN go install github.com/rhysd/actionlint/cmd/actionlint@${ACTIONLINT_VER}

# final image ->
FROM --platform=$TARGETPLATFORM scratch
COPY --from=builder /go/bin/actionlint /actionlint
ENTRYPOINT ["/actionlint"]
