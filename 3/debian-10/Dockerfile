FROM docker.io/bitnami/minideb:buster
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV HOME="/" \
    OS_ARCH="amd64" \
    OS_FLAVOUR="debian-10" \
    OS_NAME="linux"

COPY prebuildfs /
# Install required system packages and dependencies
RUN install_packages acl ca-certificates curl gzip jq libaudit1 libbsd0 libbz2-1.0 libc6 libcap-ng0 libffi6 libgcc1 libicu63 libjemalloc2 liblzma5 libncurses6 libncursesw6 libpam0g libreadline7 libsqlite3-0 libssl1.1 libstdc++6 libtinfo6 libx11-6 libxau6 libxcb1 libxdmcp6 libxml2 procps tar zlib1g
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "python" "3.8.11-0" --checksum 28b91ef5db9ad93e704881400703e4085bd82f016be15e3cf8760df044da9490
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "node" "14.17.5-0" --checksum 8afec4a09258ec4ef5f8ea6469038fa79f1d5385e055f86551d90ab4cd540a8a
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "mysql-client" "10.3.31-0" --checksum 92b99c64a3ffe10fd94ef9ecd94d2dd65a172404c726093eb50b3b293523559d
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "gosu" "1.14.0-0" --checksum 3e6fc37ca073b10a73a804d39c2f0c028947a1a596382a4f8ebe43dfbaa3a25e
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "ghost" "3.42.5-3" --checksum f6e914c37242f5593cf596e3f8eba6e5e64b58d16d537a963fe60457111b81ea
RUN chmod g+rwX /opt/bitnami

COPY rootfs /
RUN /opt/bitnami/scripts/ghost/postunpack.sh
RUN /opt/bitnami/scripts/mysql-client/postunpack.sh
ENV ALLOW_EMPTY_PASSWORD="no" \
    BITNAMI_APP_NAME="ghost" \
    BITNAMI_IMAGE_VERSION="3.42.5-debian-10-r105" \
    LD_PRELOAD="/opt/bitnami/common/lib/libnss_wrapper.so" \
    LNAME="ghost" \
    MARIADB_HOST="mariadb" \
    MARIADB_PORT_NUMBER="3306" \
    MARIADB_ROOT_PASSWORD="" \
    MARIADB_ROOT_USER="root" \
    MYSQL_CLIENT_CREATE_DATABASE_NAME="" \
    MYSQL_CLIENT_CREATE_DATABASE_PASSWORD="" \
    MYSQL_CLIENT_CREATE_DATABASE_PRIVILEGES="ALL" \
    MYSQL_CLIENT_CREATE_DATABASE_USER="" \
    MYSQL_CLIENT_ENABLE_SSL="no" \
    MYSQL_CLIENT_SSL_CA_FILE="" \
    NSS_WRAPPER_GROUP="/opt/bitnami/ghost/nss-wrapper/nss_group" \
    NSS_WRAPPER_PASSWD="/opt/bitnami/ghost/nss-wrapper/nss_passwd" \
    PATH="/opt/bitnami/python/bin:/opt/bitnami/node/bin:/opt/bitnami/mysql/bin:/opt/bitnami/common/bin:/opt/bitnami/ghost/bin:$PATH"

EXPOSE 2368 3000

WORKDIR /opt/bitnami/ghost
USER 1001
ENTRYPOINT [ "/opt/bitnami/scripts/ghost/entrypoint.sh" ]
CMD [ "/opt/bitnami/scripts/ghost/run.sh" ]
