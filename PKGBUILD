# Maintainer : SpepS <dreamspepser at yahoo dot it>
# Contributor: Ray Rashif <schiv@archlinux.org>
# Contributor: Wieland Hoffmann <the_mineo@web.de>
# Contributor: Birger Moellering <bmoellering@googlemail.com>
# Info       : <dropped from community; broken + see bug #28344>

pkgname=cwiid
pkgver=0.6.00
pkgrel=11
pkgdesc="Linux Nintendo Wiimote interface"
arch=('i686' 'x86_64')
url="http://abstrakraft.org/cwiid"
depends=('bluez>=4' 'gtk2')
license=('GPL')
install="$pkgname.install"
source=("$url/downloads/$pkgname-$pkgver.tgz"
        "$url/raw-attachment/ticket/70/bluez_4_api_changes.patch")
md5sums=('8d574afdeedc5e5309c87a72d744316a'
         '19b288723d1f2b97a3e5288ab9de3313')

build() {
  cd "$srcdir/$pkgname-$pkgver"

  # bluez v4 compatibility
  patch -Np1 -i "$srcdir/bluez_4_api_changes.patch"

  ./configure --prefix=/usr \
              --sysconfdir=/etc \
              --disable-ldconfig \
              --with-python=python2

  LDFLAGS+="$(pkg-config --libs bluez) -lrt -pthread" make
}

package() {
  cd "$srcdir/$pkgname-$pkgver"

  make DESTDIR="$pkgdir" install

  # fix static lib permissions
  chmod 644 "$pkgdir/usr/lib/libcwiid.a"

  # wminput README
  install -Dm644 wminput/README \
    "$pkgdir/usr/share/doc/$pkgname/wminput/README"
}

# vim:set ts=2 sw=2 et:
