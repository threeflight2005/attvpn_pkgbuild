# Maintainer: John Harbison <john@harbison.us>
# Contributer: Jason Gardner <buhrietoe@gmail.com>

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
source=("ftp://ftp.attglobal.net/pub/custom/ibm_linux/${pkgname}-1.0-2.0.1.${pkgver}.i386.rpm"
        'agnclientd.service')
md5sums=('b108e2ae1ca65a338f0592a2684279bf'
         '4f4a13eeee7df1b1a17bc5231c556519')

build() {
    cd "${srcdir}"

    rpmextract.sh "${pkgname}-1.0-2.0.1.${pkgver}.i386.rpm"
}

package() {
    cd "${srcdir}"

    find . -type f -exec install -D -m644 {,${pkgdir}/}{} \;
    chmod 755 $pkgdir/opt/agns/bin/*

    install -Dm644 ../agnclientd.service "${pkgdir}"/usr/lib/systemd/system/agnclientd.service
}
