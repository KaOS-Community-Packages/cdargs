pkgname=cdargs
pkgver=2.0
pkgrel=1
pkgdesc="A replacement for 'cd' that includes bookmarks/browsing for faster navigation"
arch=('x86_64')
license=('GPL')
url="http://www.skamphausen.de/cgi-bin/ska/CDargs"
screenshot="http://konsole.kde.org/images/konsole_icon_48.png"
depends=('ncurses' 'gcc-libs')
install=cdargs.install
source=("$pkgname-$pkgver.tar.gz::https://github.com/cbxbiker61/cdargs/archive/$pkgver.tar.gz")
md5sums=('93d2d0b3d9af0c3381648ec55dd11d3b')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure --prefix=/usr --mandir=/usr/share/man
  make

  cd contrib
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install-strip

  _docdir=${pkgdir}/usr/share/doc/${pkgname}
  _licdir=${pkgdir}/usr/share/licenses/${pkgname}
  install -dm755 ${_docdir} ${_licdir}
  install -Dpm644 AUTHORS ChangeLog INSTALL NEWS README THANKS TODO ${_docdir}/
  install -Dpm644 COPYING ${_licdir}/

  # install helper scripts
  cd contrib
  make DESTDIR="${pkgdir}" install
  install -d "${pkgdir}/usr/share/cdargs"
  install $pkgname-{tcsh.csh,bash.sh} "${pkgdir}/usr/share/cdargs"
}
