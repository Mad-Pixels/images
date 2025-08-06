ARG ALPINE_VERSION

# build stage ->
FROM --platform=$BUILDPLATFORM alpine:${ALPINE_VERSION} AS builder
ARG TASK_VERSION

SHELL ["/bin/ash", "-eo", "pipefail"]
RUN curl -sSL "https://github.com/go-task/task/releases/download/v${TASK_VERSION}/task_linux_$(uname -m).tar.gz" \
    | tar -xz -C /usr/local/bin task

# final image ->
FROM --platform=$TARGETPLATFORM alpine:${ALPINE_VERSION}
COPY --from=builder /usr/local/bin/task /usr/local/bin/task
ENTRYPOINT ["task"]