FROM rancher/os-rootfs
RUN ln -s /dev/null /etc/udev/rules.d/80-net-name-slot.rules
# Cleanup Buildroot
RUN rm /sbin/poweroff /sbin/reboot /sbin/halt && \
    sed -i '/^root/s!/bin/sh!/bin/bash!' /etc/passwd && \
    echo 'RancherOS \n \l' > /etc/issue && \
    rm -rf /run \
       /linuxrc \
       /etc/os-release \
       /var/cache \
       /var/lock \
       /var/log \
       /var/run \
       /var/spool \
       /var/lib/misc && \
    mkdir -p \
       /home \
       /run \
       /var/cache \
       /var/lock \
       /var/log \
       /var/run \
       /var/spool && \
    passwd -l root && \
    addgroup -g 1100 rancher && \
    addgroup -g 1101 docker && \
    addgroup -g 1103 sudo && \
    adduser -u 1100 -G rancher -D -h /home/rancher -s /bin/bash rancher && \
    adduser -u 1101 -G docker -D -h /home/docker -s /bin/bash docker && \
    sed -i 's/\(^docker.*\)/\1rancher/g' /etc/group && \
    sed -i 's/\(^sudo.*\)/\1rancher,docker/g' /etc/group && \
    echo '%sudo ALL=(ALL) ALL' >> /etc/sudoers
COPY inputrc /etc/inputrc
COPY entry.sh /usr/sbin/entry.sh

ENTRYPOINT ["/usr/sbin/entry.sh"]
