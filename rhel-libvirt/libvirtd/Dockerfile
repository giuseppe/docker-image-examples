FROM centos:latest
MAINTAINER "Brent Baude" <bbaude@redhat.com>
ENV container docker
RUN yum -y update && yum clean all
RUN rpm -e --nodeps fakesystemd
RUN yum -y install systemd 
#RUN yum -y install libvirt-daemon-driver-{network,interface,storage,qemu} qemu systemd libvirt-daemon && yum clean all; \

RUN yum install -y git libtool autoconf automake gettext-devel libtool /usr/bin/pod2man perl python systemd-units systemd-devel xen-devel libxml2-devel xhtml1-dtds libxslt readline-devel ncurses-devel gettext libtasn1-devel libgcrypt-devel gnutls-devel libattr-devel libblkid-devel augeas hal-devel systemd-devel libudev-devel libpciaccess-devel yajl-devel sanlock-devel sanlock-devel libpcap-devel libnl3-devel libnl-devel avahi-devel libselinux-devel libapparmor-devel dnsmasq iptables iptables-ipv6 radvd ebtables module-init-tools cyrus-sasl-devel polkit-devel polkit-devel PolicyKit-devel util-linux /usr/bin/qemu-img /usr/sbin/qcow-create lvm2 iscsi-initiator-utils parted-devel e2fsprogs-devel device-mapper device-mapper-devel ceph-devel glusterfs-api-devel glusterfs-deve glusterfs-api-devel glusterfs-devel numactl-devel libcap-ng-devel fuse-devel libssh2-devel netcf-devel netcf-devel netcf-devel libcurl-devel curl-devel libwsman-devel audit-libs-devel systemtap-sdt-devel util-linux nfs-utils dbus-devel gawk scrub numad wireshark-devel patch python-devel rpm-build module-init-tools numad polkit shadow-utils dbus dmidecode avahi-libs iproute libcgroup perl-XML-XPath && \
    git clone git://libvirt.org/libvirt.git && \
    (cd libvirt && git reset --hard 225f483314b64d71fc5819ee7a73f3aff3e8280b && ./autogen.sh --with-systemd-daemon --prefix=/usr --libdir=/usr/lib64) && \
    (cd libvirt && make -j4 && make -C src virtlockd.service && make -C daemon libvirtd.service && make -C tools libvirt-guests.service && \
     make install && \
     yes | cp tools/libvirt-guests.service daemon/libvirtd.service src/virtlockd.service /usr/lib/systemd/system/; ls /usr/lib/systemd/system/) && \
     (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
     rm -f /lib/systemd/system/multi-user.target.wants/*;\
     rm -f /etc/systemd/system/*.wants/*;\
     rm -f /lib/systemd/system/local-fs.target.wants/*; \
     rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
     rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
     rm -f /lib/systemd/system/basic.target.wants/*;\
     rm -f /lib/systemd/system/anaconda.target.wants/*; \
     (for i in libvirt-guests.service libvirtd.service virtlockd.service; do ln -s /usr/lib/systemd/system/$i /etc/systemd/system/$i; ln -s /usr/lib/systemd/system/$i /lib/systemd/system/multi-user.target.wants/$i; done) && \
     yum remove -y git libtool autoconf automake gettext-devel /usr/bin/pod2man systemd-devel xen-devel libxml2-devel xhtml1-dtds readline-devel ncurses-devel libtasn1-devel libgcrypt-devel gnutls-devel libattr-devel libblkid-devel hal-devel systemd-devel libudev-devel libpciaccess-devel yajl-devel sanlock-devel sanlock-devel libpcap-devel libnl3-devel libnl-devel avahi-devel libselinux-devel libapparmor-devel cyrus-sasl-devel polkit-devel polkit-devel PolicyKit-devel parted-devel e2fsprogs-devel device-mapper-devel ceph-devel glusterfs-api-devel glusterfs-deve glusterfs-api-devel glusterfs-devel numactl-devel libcap-ng-devel fuse-devel libssh2-devel netcf-devel netcf-devel netcf-devel libcurl-devel curl-devel libwsman-devel audit-libs-devel systemtap-sdt-devel dbus-devel wireshark-devel patch python-devel perl-XML-XPath && yum clean all && rm -rf libvirt && \
     mkdir -p /var/lib/libvirt/images/ && \
     sed -i "/Service/a ExecStartPost=\/bin\/chmod 666 /dev/kvm\nExecStartPre=\/bin\/rm -rf /var/run/libvirt\nExecStartPre=\/bin\/ln -s /host_run/libvirt /var/run/libvirt" /usr/lib/systemd/system/libvirtd.service

VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]
