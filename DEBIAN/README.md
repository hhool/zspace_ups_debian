#

## prepare source

```bash
git clone git@github.com:hhool/zspace_ups.git
git clone git@github.com:hhool/zspace_ups_debian.git
```

## build nut 2.8.0 to debian package

- build for ubuntu 22.04

```bash

cd zspace_ups

DEBIAN=`pwd`/../zspace_ups_debian  ./configure --prefix=/usr --sysconfdir=/etc/nut --disable-dependency-tracking --enable-strip --disable-static --with-all=no --with-usb=yes --datadir=/usr/share/nut --with-drvpath=/usr/share/nut --with-statepath=/var/run/nut --with-systemdsystemunitdir=/lib/systemd --with-systemdshutdowndir=/lib/systemd --with-systemdtmpfilesdir=/usr/lib/tmpfiles.d --with-udev-dir=/lib/udev/rules.d

make

make install DESTDIR=`pwd`/../zspace_ups_debian
```

## generate the debian package control file

```bash
dpkg -b zspace_ups_debian zspace_ups_2.8.0-signed_amd64.deb
```

## install the debian package

```bash
sudo dpkg -i zspace_ups_2.8.0-signed_amd64.deb
```

## build for arm64 rk3568 debian10

- prepare libusb

```bash
wget https://github.com/libusb/libusb/archive/refs/tags/v1.0.20.tar.gz
tar zxvf v1.0.20.tar.gz
cd  libusb-1.0.20
CC=aarch64-none-linux-gnu-gcc CXX=aarch64-none-linux-gnu-g++ ./configure --prefix=/usr --host=aarch64-none-linux-gnu --disable-udev
make
make install DESTDIR=`pwd`/../zspace_ups_debian
```

```bash
cd zspace_ups
CC=aarch64-none-linux-gnu-gcc CXX=aarch64-none-linux-gnu-g++ DEBIAN=`pwd`/../zspace_ups_debian  ./configure --prefix=/usr --sysconfdir=/etc/nut --disable-dependency-tracking --enable-strip --disable-static --with-all=no --with-usb=yes --datadir=/usr/share/nut --with-drvpath=/usr/share/nut --with-statepath=/var/run/nut --with-systemdsystemunitdir=/lib/systemd --with-systemdshutdowndir=/lib/systemd --with-systemdtmpfilesdir=/usr/lib/tmpfiles.d --with-udev-dir=/lib/udev/rules.d --with-sysroot=/opt/toolchain/gcc-arm-10.3-2021.07-x86_64-aarch64-none-linux-gnu/aarch64-none-linux-gnu/libc/ --host=aarch64-none-linux-gnu --with-usb-includes=-I$DEBIAN/usr/include/libusb-1.0 --with-usb-libs='-L'$DEBIAN'/usr/lib -lusb-1.0' --with-pkgconfig-dir=$DEBIAN/usr/lib/pkgconfig

make

make install DESTDIR=`pwd`/../zspace_ups_debian/
```
