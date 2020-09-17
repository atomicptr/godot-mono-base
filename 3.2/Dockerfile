FROM mono:6.8

# Godot build arguments
ARG GODOT_VERSION="3.2.3"
ARG GODOT_RELEASE_TAG="stable"
# set this if you want to use a non stable version like "rc1", "beta2", etc.
ARG GODOT_RELEASE_SUBDIR=""
ARG GODOT_BASE_URL="https://downloads.tuxfamily.org/godotengine/${GODOT_VERSION}/${GODOT_RELEASE_SUBDIR}/mono"
ARG GODOT_LINUX_HEADLESS_FILENAME="Godot_v${GODOT_VERSION}-${GODOT_RELEASE_TAG}_mono_linux_headless_64.zip"
ARG GODOT_LINUX_HEADLESS_URL="$GODOT_BASE_URL/$GODOT_LINUX_HEADLESS_FILENAME"
ARG GODOT_LINUX_HEADLESS_DIRECTORY_NAME="Godot_v${GODOT_VERSION}-${GODOT_RELEASE_TAG}_mono_linux_headless_64"
ARG GODOT_LINUX_HEADLESS_BINARY_NAME="Godot_v${GODOT_VERSION}-${GODOT_RELEASE_TAG}_mono_linux_headless.64"
ARG GODOT_EXPORT_TEMPLATE_FILENAME="Godot_v$GODOT_VERSION-${GODOT_RELEASE_TAG}_mono_export_templates.tpz"
ARG GODOT_EXPORT_TEMPLATE_URL="$GODOT_BASE_URL/$GODOT_EXPORT_TEMPLATE_FILENAME"

# Install dependencies
RUN apt update -qqy && \
    DEBIAN_FRONTEND=noninteractive apt install -y \
        wget \
        ca-certificates \
        git \
        python \
        python-openssl \
        zip \
        unzip && \
    # remove apt bloat
    apt clean && rm -rf /var/lib/apt/lists/*

# Setup /godot
WORKDIR /godot/tmp
RUN wget -q $GODOT_LINUX_HEADLESS_URL && \
    wget -q $GODOT_EXPORT_TEMPLATE_URL && \
    unzip -q $GODOT_LINUX_HEADLESS_FILENAME && \
    unzip -q $GODOT_EXPORT_TEMPLATE_FILENAME && \
    mv templates /godot/templates && \
    mv $GODOT_LINUX_HEADLESS_DIRECTORY_NAME /godot/engine && \
    rm -rf /godot/tmp && \
    ln -s /godot/engine/$GODOT_LINUX_HEADLESS_BINARY_NAME /usr/bin/godot && \
    mkdir -p ~/.local/share/godot/templates/ && \
    ln -s /godot/templates ~/.local/share/godot/templates/${GODOT_VERSION}.${GODOT_RELEASE_TAG}.mono

WORKDIR /
