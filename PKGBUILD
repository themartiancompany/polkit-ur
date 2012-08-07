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
source=("http://www.freedesktop.org/software/polkit/releases/$pkgname-$pkgver.tar.gz"
        'polkit.pam'
	'logind+ConsoleKit.patch'
	'autogen.sh')

build() {
  cd $pkgname-$pkgver

  patch -p1 <../logind+ConsoleKit.patch

  cp ../autogen.sh .
  ./autogen.sh --prefix=/usr --sysconfdir=/etc \
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
md5sums=('0e4f9c53f43fd1b25ac3f0d2e09b2ae1'
         '6564f95878297b954f0572bc1610dd15'
         'fb71d43442dbf24f8760198a9a79c5e7'
         '38fe3119284e842e66b330b0f2ba230d')
