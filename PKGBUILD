# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=polkit
pkgver=0.99
pkgrel=1
pkgdesc="Application development toolkit for controlling system-wide privileges"
arch=(i686 x86_64)
license=('LGPL')
url="http://www.freedesktop.org/wiki/Software/PolicyKit"
depends=('glib2>=2.26.0' 'pam' 'expat>=2.0.1')
makedepends=('intltool>=0.41.1' 'gtk-doc>=1.15' 'gobject-introspection>=0.9.5')
replaces=('policykit')
options=('!libtool')
source=(http://hal.freedesktop.org/releases/${pkgname}-${pkgver}.tar.gz
        polkit.pam)
md5sums=('fcc4d7b19c08ad54d3ce0eae0ab12398'
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
