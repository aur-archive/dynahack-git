# Maintainer: uberushaximus <uberushaximus AT gmail DOT com>

_gitname=dynahack
pkgname=${_gitname}-git
_pkgname=DynaHack
pkgver=4.0.4.r1005.g7557457
pkgrel=1
pkgdesc="A NetHack variant with UnNetHack's new content/challenges, NitroHack's UI, GruntHack's random magical items, and more"
arch=('any')
url="http://tung.github.io/${_pkgname}"
license=('custom')
depends=('jansson')
makedepends=('cmake' 'postgresql-libs' 'git')
optdepends=('postgresql-libs: to use NitroHack server')
source=(git://github.com/tung/${_pkgname}.git)
md5sums=(SKIP)

pkgver() {
  cd       "${srcdir}/${_pkgname}"
  git      describe --long | sed -E 's/([^-]*-g)/r\1/;s/-/./g'
}

build() {
  cd       "${srcdir}/${_pkgname}"
  sed   -i 's/ncursesw\///g' nitrohack/include/nhcurses.h
  cmake -DLIBDIR=/usr/lib/dynahack -DDATADIR=/var/games/dynahack -DBINDIR=/usr/lib/dynahack -DSHELLDIR=/usr/bin .
  make
}

package() {
  cd       "${srcdir}/${_pkgname}"
  make     DESTDIR="$pkgdir/" install
  chmod    775     "$pkgdir/var/games/dynahack"
  install  -Dm644  ./libnitrohack/dat/license $pkgdir/usr/share/licenses/$pkgname/LICENSE
}

# vim:set ts=2 sw=2 et:
