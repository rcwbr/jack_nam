# syntax=docker/dockerfile-upstream:master-labs

ARG BAZEL_VERSION=7.3.1

FROM gcr.io/bazel-public/bazel:${BAZEL_VERSION} AS base

FROM base AS buildifier_install
ARG BAZEL_VERSION

ADD https://github.com/bazelbuild/buildtools.git#v${BAZEL_VERSION} /tmp/buildifier
WORKDIR /tmp/buildifier
USER root
RUN --mount=type=cache,id=bazel_cache,target=/root/.cache/bazel \
  bazel \
  --output_base /tmp/bazel_out \
  build \
  --disk_cache /root/.cache/bazel \
  //buildifier

ENV PATH=${PATH}:/tmp/buildifier/bazel-bin/buildifier/buildifier_/
