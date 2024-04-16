# syntax=docker/dockerfile:1.3

FROM golang:1.22 as builder-go
ARG TARGETPLATFORM
ARG VERSION=v0.11.0
WORKDIR /workspace
RUN curl -fsSL https://github.com/knights-analytics/tokenizers/releases/download/${VERSION}/libtokenizers.$(echo ${TARGETPLATFORM} | tr / -).tar.gz | tar xvz
COPY ./example .
COPY ./test/data ./test/data
RUN go mod download
RUN mv ./libtokenizers.a /go/pkg/mod/github.com/knights-analytics/tokenizers@${VERSION}/libtokenizers.a
# mounting Go cache won't work since we mutate it above
RUN go run main.go
