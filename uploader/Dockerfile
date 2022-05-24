# Use node image based on Debian 10
FROM node:16-buster

# for Apple Silicon
# https://zenn.dev/tnzk/articles/a99b246faf5f69
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    chromium \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD=true
ENV PUPPETEER_EXECUTABLE_PATH="/usr/bin/chromium"

RUN npm install -g @kintone/plugin-uploader

# Running Puppeteer in Docker
# https://github.com/puppeteer/puppeteer/blob/main/docs/troubleshooting.md#running-puppeteer-in-docker
RUN groupadd -r pptruser \
    && useradd -r -g pptruser -G audio,video pptruser \
    && mkdir -p /home/pptruser /workspace \
    && chown -R pptruser:pptruser /home/pptruser /workspace

# Run everything after as non-privileged user.
USER pptruser
WORKDIR /workspace
CMD ["kintone-plugin-uploader", "plugin.zip"]
