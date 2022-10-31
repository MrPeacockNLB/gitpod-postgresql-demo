FROM gitpod/workspace-postgres

# Install custom tools, runtimes, etc.
# For example "bastet", a command-line tetris clone:
# RUN brew install bastet
#
# More information: https://www.gitpod.io/docs/config-docker/

RUN set -ex; \
    brew install redis; \
    brew install imagemagick; \
    brew install ghostscript; \
    brew install mailhog; \
    brew install openldap; \
    brew install lazygit; \
    sudo mkdir -p /var/log/nginx; \
    sudo chown gitpod:gitpod /var/log/nginx

# copy NginX config
COPY gitpod/files/nginx.conf /etc/nginx/nginx.conf

USER root

ENV LANG=en_US.UTF-8 \
    LC_ALL=en_US.UTF-8

RUN set -ex; \
    useradd -m -g users -s /bin/bash demo; \
    passwd demo -d; \
    echo "demo ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN set -ex; \
    apt-get -qq update; \
    apt-get -qqy install \
        gconf-service \
        libasound2 \
        libatk1.0-0 \
        libatk-bridge2.0-0 \
        libcairo2 \
        libcups2 \
        libdbus-1-3 \
        libexpat1 \
        libfontconfig1 \
        libgcc1 \
        libgconf-2-4 \
        libgdk-pixbuf2.0-0 \
        libglib2.0-0 \
        libgtk-3-0 \
        libnspr4 \
        libpango-1.0-0 \
        libpangocairo-1.0-0 \
        libx11-6 \
        libx11-xcb1 \
        libxcb1 \
        libxcomposite1 \
        libxcursor1 \
        libxdamage1 \
        libxext6 \
        libxfixes3 \
        libxi6 \
        libxrandr2 \
        libxrender1 \
        libxshmfence1 \
        libxss1 \
        libxtst6 \
        fonts-liberation \
        libappindicator1 \
        libnss3 \
        libgbm1 \
    ; \
    rm -rf /var/lib/apt/lists/*;

# switch back to user context
USER gitpod

ENV PATH="~/bin:$PATH" \
    DEMO_SMTP_ENABLED=true \
    DEMO_SMTP_HOST=localhost \
    DEMO_SMTP_PORT=1025 \
    DEMO_SMTP_USER= \
    DEMO_SMTP_PASSWORD= \
    DEMO_SMTP_SSL=false \
    DEMO_SMTP_TLS=false \
    DEMO_SMTP_DEFAULT_REPLY_TO=no-reply@example.com \
    DEMO_SMTP_DEFAULT_FROM=no-reply@example.com
