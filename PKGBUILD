# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=polkit
pkgver=0.113
pkgrel=2
pkgdesc="Application development toolkit for controlling system-wide privileges"
arch=(i686 x86_64)
license=(LGPL)
url="http://www.freedesktop.org/wiki/Software/polkit"
depends=(glib2 pam expat systemd js17)
makedepends=(intltool gtk-doc gobject-introspection git)
install=polkit.install
source=(http://www.freedesktop.org/software/polkit/releases/$pkgname-$pkgver.tar.gz)
md5sums=('4b77776c9e4f897dcfe03b2c34198edf')

build() {
  cd $pkgname-$pkgver

  ./configure --prefix=/usr --sysconfdir=/etc \
      --localstatedir=/var --libexecdir=/usr/lib/polkit-1 \
      --enable-libsystemd-login=yes --disable-static \
      --enable-gtk-doc --with-os-type=redhat
  make
}

check() {
  cd $pkgname-$pkgver
  make -k check || :
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install

  chown 102 "$pkgdir/etc/polkit-1/rules.d"
  chown 102 "$pkgdir/usr/share/polkit-1/rules.d"
}
