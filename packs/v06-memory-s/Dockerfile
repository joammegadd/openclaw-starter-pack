FROM ghcr.io/openclaw/openclaw:latest

USER root

# instala dependências mínimas para baixar o uv
RUN apt-get update && apt-get install -y curl ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# instala o uv em local fixo e coloca no PATH
RUN curl -LsSf https://astral.sh/uv/install.sh | env UV_UNMANAGED_INSTALL="/usr/local/bin" sh

# valida instalação
RUN uv --version

USER node