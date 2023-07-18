FROM rust:1
ARG USER=worker
ARG USER_UID=1000
ARG USER_GID=1000

ENV TZ=Asia/Tokyo
RUN apt-get update && apt-get install tzdata -y && \
    echo 'Asia/Tokyo' > /etc/timezone && \
    dpkg-reconfigure tzdata && apt-get clean && rm -fr /var/apt/cache /var/lib/apt
RUN ln -sf usr/share/zoneinfo/Asia/Tokyo /etc/localtime
RUN apt-get update && apt-get install locales -y && \
    echo 'ja_JP.UTF-8 UTF-8' >> /etc/locale.gen && \
    locale-gen ja_JP.UTF-8 && update-locale && apt-get clean && rm -fr /var/apt/cache /var/lib/apt
ENV LC_ALL=ja_JP.UTF-8

RUN apt-get update && apt-get install -y sudo && \
    apt-get clean && rm -fr /var/apt/cache /var/lib/apt
RUN groupadd -g "${USER_GID}" "${USER}"
RUN useradd -u "${USER_UID}" -g "${USER_GID}" -s /bin/bash -G sudo -m "${USER}"
RUN echo "${USER} ALL = (ALL)NOPASSWD:ALL" > /etc/sudoers.d/"${USER}" && \
    chmod 400 /etc/sudoers.d/"${USER}"
USER ${USER}
