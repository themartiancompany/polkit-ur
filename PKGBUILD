# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=polkit
pkgver=0.107
pkgrel=1
pkgdesc="Application development toolkit for controlling system-wide privileges"
arch=(i686 x86_64)
license=('LGPL')
url="http://www.freedesktop.org/wiki/Software/PolicyKit"
depends=('glib2' 'pam' 'expat' 'libsystemd' 'js')
makedepends=('intltool' 'gtk-doc' 'gobject-introspection')
replaces=('policykit')
options=('!libtool')
install=polkit.install
source=(http://www.freedesktop.org/software/polkit/releases/$pkgname-$pkgver.tar.gz
        polkit.pam)
md5sums=('0e4f9c53f43fd1b25ac3f0d2e09b2ae1'
         '6564f95878297b954f0572bc1610dd15')

build() {
  cd $pkgname-$pkgver

  ./configure --prefix=/usr --sysconfdir=/etc \
      --localstatedir=/var --libexecdir=/usr/lib/polkit-1 \
      --with-systemdsystemunitdir=/usr/lib/systemd/system \
      --disable-static --enable-gtk-doc
  make
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install

  chown 102 "$pkgdir/etc/polkit-1/rules.d"
  chown 102 "$pkgdir/usr/share/polkit-1/rules.d"

  install -m644 "$srcdir/polkit.pam" "$pkgdir/etc/pam.d/polkit-1"
}
