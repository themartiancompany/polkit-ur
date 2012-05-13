# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=polkit
pkgver=0.105
pkgrel=1
pkgdesc="Application development toolkit for controlling system-wide privileges"
arch=(i686 x86_64)
license=('LGPL')
url="http://www.freedesktop.org/wiki/Software/PolicyKit"
depends=('glib2' 'pam' 'expat')
makedepends=('intltool' 'gtk-doc' 'gobject-introspection')
replaces=('policykit')
options=('!libtool')
source=(http://www.freedesktop.org/software/polkit/releases/$pkgname-$pkgver.tar.gz
        polkit.pam)
md5sums=('9c29e1b6c214f0bd6f1d4ee303dfaed9'
         '6564f95878297b954f0572bc1610dd15')

build() {
  cd $pkgname-$pkgver
  ./configure --prefix=/usr --sysconfdir=/etc \
      --localstatedir=/var --libexecdir=/usr/lib/polkit-1 \
      --disable-static --enable-gtk-doc
  make
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install

  install -m644 "$srcdir/polkit.pam" "$pkgdir/etc/pam.d/polkit-1"
}
