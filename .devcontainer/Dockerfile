FROM mcr.microsoft.com/vscode/devcontainers/base:bullseye

WORKDIR /opt

# Rye を使える様に Path を通す
ENV RYE_HOME="/opt/rye"
ENV PATH="$RYE_HOME/shims:$PATH"

# hadolint ignore=DL3008
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        curl

# curl を使って Rye をダウンロードする
SHELL [ "/bin/bash", "-o", "pipefail", "-c" ]
RUN curl -sSf https://rye-up.com/get | RYE_INSTALL_OPTION="--yes" bash && \
    rye config --set-bool behavior.global-python=true && \
    # パッケージ管理(pipなど)にuvを使う
    rye config --set-bool behavior.use-uv=true

RUN chown -R vscode $RYE_HOME