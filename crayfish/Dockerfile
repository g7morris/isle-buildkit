# syntax=docker/dockerfile:experimental
FROM local/nginx:latest

ARG COMMIT=1.1.1

RUN --mount=id=downloads,type=cache,target=/opt/downloads \
    DOWNLOAD_CACHE_DIRECTORY="/opt/downloads" && \
    git-clone-cached.sh \
        --url https://github.com/Islandora/Crayfish.git \
        --cache-dir "${DOWNLOAD_CACHE_DIRECTORY}" \
        --commit "${COMMIT}" \
        --worktree /var/www/crayfish && \
    mkdir /var/log/islandora && \
    mkdir -p /opt/keys/jwt && \
    chown nginx:nginx /var/log/islandora && \
    chown nginx:nginx /opt/keys/jwt && \
    chown -R nginx:nginx /var/www && \
    cleanup.sh

COPY /rootfs /

STOPSIGNAL SIGWINCH

EXPOSE 8000
