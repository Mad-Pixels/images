ARG ALPINE_VERSION

# build stage ->
FROM --platform=$BUILDPLATFORM alpine:${ALPINE_VERSION} AS builder
ARG TASK_VERSION

RUN apk add --no-cache go git 
ENV GOPATH=/go \
    GOCACHE=/tmp/.cache \
    PATH=/go/bin:/usr/local/go/bin:$PATH
RUN go install github.com/go-task/task/v3/cmd/task@${TASK_VERSION}

# final image ->
FROM --platform=$TARGETPLATFORM alpine:${ALPINE_VERSION}
COPY --from=builder /go/bin/task /usr/local/bin/task
RUN apk add --no-cache git 

ENTRYPOINT ["task"]
