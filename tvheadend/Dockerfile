ARG BUILD_FROM
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

COPY requirements.txt /tmp/

RUN \
    apk update \
    && apk add --no-cache --virtual .build-deps \
    musl-dev=1.2.5-r21 \
    gcc=15.2.0-r2  \
    g++=15.2.0-r2 \
    libxml2-dev=2.13.9-r0 \
    libxslt-dev=1.1.43-r3 \
    python3-dev=3.12.12-r0 \
    && apk add --no-cache \
    tvheadend=4.3_git20251018-r0 \
    py3-pip=25.1.1-r1 \
    libxslt=1.1.43-r3 \
    && pip3 install \
    --no-cache-dir \
    --prefer-binary \
    -r /tmp/requirements.txt \
    && apk del --no-cache --purge .build-deps

# Copy root filesystem
COPY rootfs /

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Nagy V <126671+nagyv@users.noreply.github.com>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="NagyV" \
    org.opencontainers.image.authors="Nagy V <126671+nagyv@users.noreply.github.com>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://github.com/NagyV/addon-tvheadend" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
