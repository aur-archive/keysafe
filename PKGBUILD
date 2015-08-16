# $Id: PKGBUILD 51798 2011-07-15 11:51:19Z spupykin $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Magnus Therning <magnus@therning.org>

pkgname=keysafe
pkgver=0.5
pkgrel=3
pkgdesc="A safe place to keep your passwords"
arch=('i686' 'x86_64')
url="http://therning.org/magnus/computer/keysafe/"
license=('GPL')
depends=('gnome-python' 'boost-libs' 'botan')
makedepends=('boost' 'cython')
install=keysafe.install
options=(!libtool !emptydirs)
source=($pkgname-$pkgver.tar.gz::http://github.com/magthe/keysafe/tarball/v$pkgver
	build-fix.patch)
md5sums=('f21921888a5ea5483dd849e2a5ed924d'
         '128d71e889ebe8862e297bbfd2079c77')

build() {
  cd ${srcdir}/magthe-keysafe*
  patch -p1 <$srcdir/build-fix.patch
  ./waf configure --prefix=/usr
  ./waf build
}

package() {
  cd ${srcdir}/magthe-keysafe*
  ./waf --destdir=${pkgdir} install
  install -m755 -d "${pkgdir}/usr/share/gconf/schemas"
  gconf-merge-schema "${pkgdir}/usr/share/gconf/schemas/${pkgname}.schemas" ${pkgdir}/etc/gconf/schemas/*.schemas
  rm -f ${pkgdir}/etc/gconf/schemas/*.schemas
  rm -f ${pkgdir}/usr/etc/gconf/schemas/*.schemas
}
