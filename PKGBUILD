# $Id: PKGBUILD 62512 2012-01-20 09:51:29Z spupykin $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Maintainer: William Rea <sillywilly@gmail.com>
# Contributor: Hans Janssen <hans@janserv.xs4all.nl>

pkgname=flightgear-atlas
pkgver=0.3.1
pkgrel=5
arch=(i686 x86_64)
pkgdesc="aims to produce and display high quality charts of the world for users of FlightGear."
depends=('libpng' 'libjpeg')
makedepends=('simgear')
url="http://atlas.sourceforge.net"
license=('GPL')
source=(http://downloads.sourceforge.net/sourceforge/atlas/Atlas-$pkgver.tar.gz
	build-fix.patch)
md5sums=('15bba54523a29928a14f17af449f960e'
         '6ad0d34b617d9ca680a63c965479eb7c')

build() {
  depends=('flightgear-data' 'libpng' 'libjpeg')

  cd $srcdir/Atlas-$pkgver

  sed -i 's|png_ptr->jmpbuf|png_jmpbuf(png_ptr)|g' src/OutputGL.cxx
  patch -p1 <$srcdir/build-fix.patch
  LDFLAGS="-lsgstructure" ./configure --prefix=/usr
  perl -ne 's/LIBS =(.+)/LIBS =$1 -lsgstructure/g; print;' src/Makefile >src/Makefile2
  mv src/Makefile2 src/Makefile

  make
  make DESTDIR=$pkgdir install
  mkdir -p $pkgdir/usr/share/FlightGear/data
  cp $srcdir/Atlas-$pkgver/src/AtlasPalette $pkgdir/usr/share/FlightGear/data
}
