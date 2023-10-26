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
