FROM debian:stretch-slim
# FROM arm64=skip

# qga version 2.8.1
RUN apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -y qemu-guest-agent \
    && apt-get clean \
    && rm -rf /var/lib/apt/*
ADD run /usr/local/bin/

ENTRYPOINT ["/usr/bin/ros", "entrypoint"]

RUN addgroup --gid 1100 burmilla && \
    addgroup --gid 1101 docker && \
    adduser -q -u 1100 --gid 1100 --shell /bin/bash burmilla && \
    adduser -q -u 1101 --gid 1101 --shell /bin/bash docker && \
    adduser docker sudo && \
    sed -i 's/burmilla:!/burmilla:*/g' /etc/shadow && \
    sed -i 's/docker:!/docker:*/g' /etc/shadow && \
    echo '## allow password less for burmilla user' >> /etc/sudoers && \
    echo 'burmilla ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers && \
    echo '## allow password less for docker user' >> /etc/sudoers && \
    echo 'docker ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers && \
    echo "docker:tcuser" | chpasswd
