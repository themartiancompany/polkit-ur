# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=polkit
pkgver=0.104
pkgrel=2
pkgdesc="Application development toolkit for controlling system-wide privileges"
arch=(i686 x86_64)
license=('LGPL')
url="http://www.freedesktop.org/wiki/Software/PolicyKit"
depends=('glib2' 'pam' 'expat' 'libsystemd')
makedepends=('intltool' 'gtk-doc' 'gobject-introspection')
replaces=('policykit')
options=('!libtool')
source=(http://hal.freedesktop.org/releases/$pkgname-$pkgver.tar.gz
        polkit.pam systemd-fallback.patch)
md5sums=('e380b4c6fb1e7bccf854e92edc0a8ce1'
         '6564f95878297b954f0572bc1610dd15'
         '3c89d97a329ab0ea3a9248c68c3ab000')

build() {
  cd $pkgname-$pkgver
  patch -Np1 -i ../systemd-fallback.patch
  autoreconf -f -i
  ./configure --prefix=/usr --sysconfdir=/etc \
      --localstatedir=/var --libexecdir=/usr/lib/polkit-1 \
      --disable-static --enable-gtk-doc --enable-systemd
  make
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install

  install -m644 "$srcdir/polkit.pam" "$pkgdir/etc/pam.d/polkit-1"
}
