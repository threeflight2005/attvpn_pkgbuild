# Maintainer: John Harbison <john@harbison.us>
pkgname=agnclient
pkgver=3003
pkgrel=1
pkgdesc="A port of the ATT VPN client binary to run on Arch"
arch=('i686' 'x86_64')
url="http://www.attglobal.net/"
license=('unknown')
depends=('libidn'
         'lib32-glibc'
         'lib32-atk'
         'lib32-openssl'
         'lib32-curl'
         'lib32-gcc-libs'
         'lib32-gtk2'
         'lib32-gdk-pixbuf2'
         'lib32-glib2'
         'lib32-pango'
         'lib32-pangox-compat'
         'lib32-libxml2'
         'tcl')
makedepends=('rpmextract')
options=('emptydirs')
source=("ftp://ftp.attglobal.net/pub/custom/ibm_linux/${pkgname}-1.0-2.0.1.${pkgver}.i386.rpm")
md5sums=('b108e2ae1ca65a338f0592a2684279bf')

build() {
  rpmextract.sh ${pkgname}-1.0-2.0.1.${pkgver}.i386.rpm
  rm ${pkgname}-1.0-2.0.1.${pkgver}.i386.rpm
  rm ../${pkgname}-1.0-2.0.1.${pkgver}.i386.rpm
}

package() {
 find . -type f -exec install -D -m 644 {,${pkgdir}/}{} \;
 chmod 755 $pkgdir/opt/agns/bin/*
 mkdir -p -m 755 $pkgdir/usr/lib32/

 if [ !/usr/lib32/libpangox-1.0.so.0 ]
 then
     ln -s /usr/lib/libpangox-1.0.so.0 $pkgdir/usr/lib32/libpangox-1.0.so.0
 elif [ /usr/lib32/libpangox-1.0.so.0 ]
 then
     echo "/usr/lib32/libpangox-1.0.so.0 exist"
 fi

 if [ !/usr/lib32/libssl.so.4 ]
 then
     ln -s /usr/lib32/libssl.so $pkgdir/usr/lib32/libssl.so.4
 elif [ /usr/lib32/libssl.so.4 ]
 then
     echo "/usr/lib32/libssl.so.4 exits"
 fi

 mkdir -p -m 755 $pkgdir/usr/lib/systemd/system/

 echo "[Unit]
 Description="ATT VPN service daemon"

 [Service]
 ExecStart=/opt/agns/bin/agnclientd
 ExecStop=if [ /var/run/agnclientd.pid ] ; then /usr/bin/kill -9 `cat /var/run/agnclientd.pid` ; elif [ !/var/run/agnclientd.pid ] ; then exit 0 ; fi
 PIDfile=/var/run/agnclientd.pid

 [Install]
 WantedBy=multi-user.target" > $pkgdir/usr/lib/systemd/system/agnclientd.service

 chmod 755 $pkgdir/usr/lib/systemd/system/agnclientd.service
}
