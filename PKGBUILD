# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=polkit
pkgver=0.109
pkgrel=1
pkgdesc="Application development toolkit for controlling system-wide privileges"
arch=(i686 x86_64)
license=('LGPL')
url="http://www.freedesktop.org/wiki/Software/polkit"
depends=('glib2' 'pam' 'expat' 'libsystemd' 'js')
makedepends=('intltool' 'gtk-doc' 'gobject-introspection')
replaces=('policykit')
options=('!libtool')
install=polkit.install
source=(http://www.freedesktop.org/software/polkit/releases/$pkgname-$pkgver.tar.gz
        polkit.pam
        fix-xauthority.patch)
md5sums=('8c3f08287dd3e1e546e3c2ae00090908'
         '6564f95878297b954f0572bc1610dd15'
         '78db344a30d7aa089b4705009ec95b58')

build() {
  cd $pkgname-$pkgver

  patch -Np1 -i ../fix-xauthority.patch

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
