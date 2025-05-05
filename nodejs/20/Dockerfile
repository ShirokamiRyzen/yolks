FROM        --platform=$TARGETOS/$TARGETARCH node:20-bookworm-slim

LABEL       author="Shirokami Ryzen" maintainer="ryzendesu.vip@gmail.com"

# Tambahkan user container
RUN         useradd -m -d /home/container container
STOPSIGNAL  SIGINT

# Install semua dependencies termasuk Chromium
RUN         apt update && apt -y install \
    ffmpeg \
    iproute2 \
    git \
    sqlite3 \
    libsqlite3-dev \
    python3 \
    python3-dev \
    ca-certificates \
    dnsutils \
    tzdata \
    zip \
    tar \
    curl \
    build-essential \
    libtool \
    iputils-ping \
    libnss3 \
    tini \
    imagemagick \
    wget \
    gnupg \
    fonts-liberation \
    fonts-noto-color-emoji \
    libfontconfig1 \
    fontconfig \
    libappindicator3-1 \
    libasound2 \
    libatk-bridge2.0-0 \
    libatk1.0-0 \
    libgtk-3-0 \
    libnspr4 \
    libx11-xcb1 \
    libxcomposite1 \
    libxcursor1 \
    libxdamage1 \
    libxi6 \
    libxrandr2 \
    libxshmfence1 \
    libxss1 \
    libxtst6 \
    lsb-release \
    x11-utils \
    libgbm-dev \
    chromium \
    chromium-driver \
    --no-install-recommends \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install tools tambahan (opsional)
RUN         npm install --global typescript ts-node @types/node

# Install pnpm
RUN         npm install -g corepack \
    && corepack enable \
    && corepack prepare pnpm@latest --activate

# Pindah ke user container biasa
USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

# Salin dan izinkan entrypoint
COPY        --chown=container:container ./../entrypoint.sh /entrypoint.sh
RUN         chmod +x /entrypoint.sh

ENTRYPOINT  ["/usr/bin/tini", "-g", "--"]
CMD         ["/entrypoint.sh"]
