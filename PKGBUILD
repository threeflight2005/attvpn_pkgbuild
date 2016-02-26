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
install='agnclient.install'

build() {
  rpmextract.sh ${pkgname}-1.0-2.0.1.${pkgver}.i386.rpm
  rm ${pkgname}-1.0-2.0.1.${pkgver}.i386.rpm
  rm ../${pkgname}-1.0-2.0.1.${pkgver}.i386.rpm
}

package() {
 find . -type f -exec install -D -m 644 {,${pkgdir}/}{} \;
 chmod 755 $pkgdir/opt/agns/bin/*
 mkdir -p -m 755 $pkgdir/usr/lib32/

 if [ -e /usr/lib32/libpangox-1.0.so.0 ]
 then
     echo "/usr/lib32/libpangox-1.0.so.0 exist"
 else
   ln -s /usr/lib/libpangox-1.0.so.0 $pkgdir/usr/lib32/libpangox-1.0.so.0
 fi

 if [ -e /usr/lib32/libssl.so.4 ]
 then
     echo "/usr/lib32/libssl.so.4 exits"
 else
     ln -s /usr/lib32/libssl.so $pkgdir/usr/lib32/libssl.so.4
 fi

 if [ -e /usr/lib32/libcrypto.so.4 ]
 then
     echo "/usr/lib32/libssl.so.4 exits"
 else
     ln -s /usr/lib32/libcrypto.so.1.0.0 $pkgdir/usr/lib32/libcrypto.so.4
 fi

 mkdir -p -m 755 $pkgdir/usr/lib/systemd/system/

 install -m644  $startdir/agnclientd.service ${pkgdir}/usr/lib/systemd/system || return 1

}
