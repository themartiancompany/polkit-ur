# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=polkit
pkgver=0.112
pkgrel=4
pkgdesc="Application development toolkit for controlling system-wide privileges"
arch=(i686 x86_64)
license=(LGPL)
url="http://www.freedesktop.org/wiki/Software/polkit"
depends=(glib2 pam expat systemd js17)
makedepends=(intltool gtk-doc gobject-introspection git)
install=polkit.install
source=("git://anongit.freedesktop.org/polkit#commit=fb5076b7c05d01a532d593a4079a29cf2d63a228"
        polkit.pam)
md5sums=('SKIP'
         '6564f95878297b954f0572bc1610dd15')

build() {
  cd $pkgname

  NOCONFIGURE=1 ./autogen.sh

  ./configure --prefix=/usr --sysconfdir=/etc \
      --localstatedir=/var --libexecdir=/usr/lib/polkit-1 \
      --enable-libsystemd-login=yes --disable-static \
      --enable-gtk-doc
  make
}

package() {
  cd $pkgname
  make DESTDIR="$pkgdir" install

  chown 102 "$pkgdir/etc/polkit-1/rules.d"
  chown 102 "$pkgdir/usr/share/polkit-1/rules.d"

  install -m644 "$srcdir/polkit.pam" "$pkgdir/etc/pam.d/polkit-1"
}
