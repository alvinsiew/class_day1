ARG GO_VER=1.17

FROM golang:${GO_VER} AS builder

ARG APP_DIR=/app

WORKDIR ${APP_DIR}

ADD main.go .
ADD go.mod .
ADD go.sum .

RUN go build -o main main.go

FROM golang:${GO_VER}

ARG APP_DIR=/app

WORKDIR ${APP_DIR}

COPY --from=builder ${APP_DIR}/main .
ADD public public
ADD templates templates

ENV APP_PORT=3000 INSTANCE_NAME="dov-go-bear"

EXPOSE ${APP_PORT}

ENTRYPOINT [ "./main" ]


# HEALTHCHECK  --interval=5m --timeout=3s \
#     CMD wget --no-verbose --tries=1 --spider http://localhost:3000/healthz || exit 1

# CMD "./main"
# RUN ["./main"] 