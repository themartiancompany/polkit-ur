# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=polkit
pkgver=0.95
pkgrel=1
pkgdesc="Application development toolkit for controlling system-wide privileges"
arch=(i686 x86_64)
license=('LGPL')
url="http://www.freedesktop.org/wiki/Software/Policykit"
depends=('eggdbus>=0.6' 'pam')
makedepends=('intltool' 'gtk-doc' 'gobject-introspection')
options=('!libtool')
source=(http://hal.freedesktop.org/releases/${pkgname}-${pkgver}.tar.gz
        polkit.pam)
md5sums=('10971f5d334550025897b02d779fddd1'
         '6564f95878297b954f0572bc1610dd15')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure --prefix=/usr --sysconfdir=/etc \
      --localstatedir=/var --libexecdir=/usr/lib/polkit-1 \
      --disable-static --enable-gtk-doc || return 1
  make || return 1
  make DESTDIR="${pkgdir}" install || return 1

  install -m644 "${srcdir}/polkit.pam" "${pkgdir}/etc/pam.d/polkit-1" || return 1
}
