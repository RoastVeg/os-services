FROM rancher/os-fedoraconsole-base
# FROM amd64=fedora:24 arm64=skip arm=skip
RUN dnf install -y iptables openssh-server rsync sudo vim less ca-certificates psmisc htop procps-ng \
    && rm -rf /etc/ssh/*key* \
    && ln -s /sbin/agetty /sbin/getty
RUN groupadd --gid 1100 rancher \
    && groupadd --gid 1101 docker \
    && useradd -u 1100 -g rancher -G docker,wheel -m -s /bin/bash rancher \
    && useradd -u 1101 -g docker -G docker,wheel -m -s /bin/bash docker \
    && echo ClientAliveInterval 180 >> /etc/ssh/sshd_config \
    && echo '## allow password less for rancher user' >> /etc/sudoers \
    && echo 'rancher ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers \
    && echo '## allow password less for docker user' >> /etc/sudoers \
    && echo 'docker ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers
COPY prompt.sh /etc/profile.d/
ENTRYPOINT ["/usr/bin/ros", "entrypoint"]