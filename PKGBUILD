# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=polkit
pkgver=0.103
pkgrel=1
pkgdesc="Application development toolkit for controlling system-wide privileges"
arch=(i686 x86_64)
license=('LGPL')
url="http://www.freedesktop.org/wiki/Software/PolicyKit"
depends=('glib2' 'pam' 'expat')
makedepends=('intltool' 'gtk-doc' 'gobject-introspection')
replaces=('policykit')
options=('!libtool')
source=(http://hal.freedesktop.org/releases/${pkgname}-${pkgver}.tar.gz
        polkit.pam)
md5sums=('aaacf2ef18774ea8a825a426a7cfe763'
         '6564f95878297b954f0572bc1610dd15')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure --prefix=/usr --sysconfdir=/etc \
      --localstatedir=/var --libexecdir=/usr/lib/polkit-1 \
      --disable-static --enable-gtk-doc
  make
  make DESTDIR="${pkgdir}" install

  install -m644 "${srcdir}/polkit.pam" "${pkgdir}/etc/pam.d/polkit-1"
}
