# Debian

## build zspace_ups to debian package

```bash
mkdir zspace_ups_debian

cd zspace_ups
DEBIAN=/workspaces/codespaces-blank/zspace_ups_debian && sudo ./configure --prefix=$DEBIAN/usr --sysconfdir=$DEBIAN/etc/nut --disable-dependency-tracking --enable-strip --disable-static --with-all=no --with-usb=yes --datadir=$DEBIAN/usr/share/nut --with-drvpath=$DEBIAN/usr/share/nut --with-statepath=$DEBIAN/var/run/nut --with-systemdsystemunitdir=$DEBIAN/lib/systemd --with-systemdshutdowndir=$DEBIAN/lib/systemd --with-systemdtmpfilesdir=$DEBIAN/usr/lib/tmpfiles.d --with-udev-dir=$DEBIAN/lib/udev/rules.d

make

make install
```

## generate the debian package control file

```bash
cd workspaces/codespaces-blank
sudo dpkg -b zspace_ups_debian zspace_ups_2.8.0-signed_amd64.deb
```

## install the debian package

```bash
sudo dpkg -i zspace_ups_2.8.0-signed_amd64.deb
```

## build for arm64 rk3568

- prepare libusb

```bash
  wget https://github.com/libusb/libusb/archive/refs/tags/v1.0.20.tar.gz
  tar zxvf v1.0.20.tar.gz
  cd  libusb-1.0.20
  DEBIAN=/home/hhool/Desktop/nut/zspace_ups_debian ./configure --prefix=$DEBIAN/usr --host=aarch64-none-linux-gnu
```

```bash
DEBIAN=/home/hhool/Desktop/nut/zspace_ups_debian ./configure --prefix=$DEBIAN/usr --syscon
fdir=$DEBIAN/etc/nut --disable-dependency-tracking --enable-strip --disable-static --with-all=no --with-usb=no --datadir=$DEBIAN/usr/share/nut --with-drv
path=$DEBIAN/usr/share/nut --with-statepath=$DEBIAN/var/run/nut --with-systemdsystemunitdir=$DEBIAN/lib/systemd --with-systemdshutdowndir=$DEBIAN/lib/sys
temd --with-systemdtmpfilesdir=$DEBIAN/usr/lib/tmpfiles.d --with-udev-dir=$DEBIAN/lib/udev/rules.d --with-sysroot=/opt/toolchain/gcc-arm-10.3-2021.07-x86
_64-aarch64-none-linux-gnu/aarch64-none-linux-gnu/libc/ --host=aarch64-none-linux-gnu
```
