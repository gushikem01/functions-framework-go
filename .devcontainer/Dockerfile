# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.187.0/containers/go/.devcontainer/base.Dockerfile

# [Choice] Go version: 1, 1.16, 1.15
ARG VARIANT="1.16"
FROM mcr.microsoft.com/vscode/devcontainers/go:0-${VARIANT}

# [Option] Install Node.js
ARG INSTALL_NODE="true"
ARG NODE_VERSION="lts/*"
RUN if [ "${INSTALL_NODE}" = "true" ]; then su vscode -c "umask 0002 && . /usr/local/share/nvm/nvm.sh && nvm install ${NODE_VERSION} 2>&1"; fi

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
# [Optional] Uncomment this section to install additional OS packages.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
  && apt-get -y install --no-install-recommends zip g++ unzip

RUN echo "deb [arch=amd64] http://storage.googleapis.com/bazel-apt stable jdk1.8" | sudo tee /etc/apt/sources.list.d/bazel.list && \
  curl https://bazel.build/bazel-release.pub.gpg | sudo apt-key add - && \
  apt update && \
  apt -y install bazel && \
  apt -y install patch

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# [Optional] Uncomment the next line to use go get to install anything else you need
# RUN go get -x <your-dependency-or-tool>

# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1
ENV GO111MODULE=off

# RUN go get -u github.com/GoogleCloudPlatform/functions-framework-go
ENV GO111MODULE on

ENV GO_ENV="development"

COPY ./entrypoint.sh /entrypoint.sh
RUN chmod 0755 /entrypoint.sh
# コンテナ起動時の処理
ENTRYPOINT ["/entrypoint.sh"]