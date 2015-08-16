# $Id$
# Maintainer: Chris Brannon <cmbrannon79@gmail.com>
# Contributor: Andrea Scarpino <andrea@archlinux.org>
# Contributor: Anders Bergh <anders1@gmail.com>
# Contributor: Dawid Ciezarkiewicz <dawid.ciezarkiewicz@jabster.pl>

pkgname=libphobos
pkgver=1.072
pkgrel=1
pkgdesc="Runtime library for the D programming language"
arch=('i686' x86_64)
url="http://www.digitalmars.com/d/1.0/"
source=(http://ftp.digitalmars.com/dmd.$pkgver.zip dmd.conf)
depends=(dmd=$pkgver)
license=('custom')
conflicts=('libtango')

build() {
  install -d "$pkgdir/usr/include/d"
  cd "$srcdir/dmd/src/phobos"
  cp -Rf std "$pkgdir/usr/include/d"
  cp -Rf etc "$pkgdir/usr/include/d"
  cp -Rf internal "$pkgdir/usr/include/d"
  cp -f {crc32,object,gcstats}.d "$pkgdir/usr/include/d"

  if [ $CARCH == x86_64 ]; then
    install -Dm644 "$srcdir/dmd/linux/lib64/libphobos.a" "$pkgdir/usr/lib/libphobos.a"
  else
    install -Dm644 "$srcdir/dmd/linux/lib32/libphobos.a" "$pkgdir/usr/lib/libphobos.a"
  fi

  install -Dm644 "$srcdir/dmd.conf" "$pkgdir/etc/dmd.conf"

  # Get rid of this subdirectory; it's just an unpacked zlib source
  # distribution.
  rm -rf "${pkgdir}/usr/include/d/etc/c/zlib"
  # Insure that files and directories under /usr/include/d have
  # correct permissions.
  find "${pkgdir}/usr/include/d" -type d -print0 |xargs -0 chmod 755
  find "${pkgdir}/usr/include/d" -type f -print0 |xargs -0 chmod 644
  install -Dm644 phoboslicense.txt "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

md5sums=('d5489b94f06c7ca2f4b5de62f7e6815a'
         'e93f0ccb1e5c00cd222af5a9be3f599a')
