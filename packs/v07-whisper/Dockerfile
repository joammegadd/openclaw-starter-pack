FROM ghcr.io/openclaw/openclaw:latest

USER root

RUN apt-get update && apt-get install -y \
    curl \
    ca-certificates \
    ffmpeg \
    git \
    cmake \
    build-essential \
    libavcodec-dev \
    libavformat-dev \
    libavutil-dev \
    && rm -rf /var/lib/apt/lists/*

RUN curl -LsSf https://astral.sh/uv/install.sh | env UV_UNMANAGED_INSTALL="/usr/local/bin" sh

WORKDIR /opt
RUN git clone https://github.com/ggml-org/whisper.cpp.git
WORKDIR /opt/whisper.cpp

RUN cmake -B build -DWHISPER_FFMPEG=yes
RUN cmake --build build --config Release

# RUN mkdir -p /opt/whisper.cpp/models && \
#     curl -L https://huggingface.co/ggerganov/whisper.cpp/resolve/main/ggml-small.bin \
#     -o /opt/whisper.cpp/models/ggml-small.bin

ENV PATH="/opt/whisper.cpp/build/bin:${PATH}"
ENV WHISPER_CPP_MODEL="/opt/whisper.cpp/models/ggml-base.bin"

USER node
WORKDIR /app