FROM debian:bookworm

# 日本のミラーサーバを使用（セキュリティは公式を使用）
RUN echo "deb http://ftp.jaist.ac.jp/pub/Linux/debian/ bookworm main non-free-firmware non-free contrib" > /etc/apt/sources.list && \
    echo "deb http://ftp.jaist.ac.jp/pub/Linux/debian/ bookworm-updates main non-free-firmware non-free contrib" >> /etc/apt/sources.list && \
    echo "deb http://security.debian.org/debian-security bookworm-security main non-free-firmware non-free contrib" >> /etc/apt/sources.list

# オプション2: 理化学研究所 (RIKEN) - 高速で安定
# RUN echo "deb http://ftp.riken.jp/Linux/debian/ bookworm main non-free-firmware non-free contrib" > /etc/apt/sources.list && \
#     echo "deb http://ftp.riken.jp/Linux/debian/ bookworm-updates main non-free-firmware non-free contrib" >> /etc/apt/sources.list && \
#     echo "deb http://ftp.riken.jp/Linux/debian-security/ bookworm-security main non-free-firmware non-free contrib" >> /etc/apt/sources.list

# オプション3: IIJ (Internet Initiative Japan)
# RUN echo "deb http://ftp.jp.debian.org/debian/ bookworm main non-free-firmware non-free contrib" > /etc/apt/sources.list && \
#     echo "deb http://ftp.jp.debian.org/debian/ bookworm-updates main non-free-firmware non-free contrib" >> /etc/apt/sources.list && \
#     echo "deb http://ftp.jp.debian.org/debian-security/ bookworm-security main non-free-firmware non-free contrib" >> /etc/apt/sources.list

RUN apt-get update -y && apt-get -y --allow-unauthenticated install debos \
    xz-utils dosfstools libterm-readkey-perl user-mode-linux libslirp-helper \
    && apt install -y -f

RUN apt-get update -y && \
    apt-get install -y --no-install-recommends vim ssh ssh-import-id git tree \
    debian-keyring gpgv network-manager host curl bmap-tools

# add credentials on build
ARG SSH_PRIVATE_KEY
RUN mkdir /root/.ssh/
RUN echo "${SSH_PRIVATE_KEY}" > /root/.ssh/id_rsa && chmod 600 /root/.ssh/id_rsa
RUN touch /root/.ssh/known_hosts

ENV USER=root \
    HOME=/root
