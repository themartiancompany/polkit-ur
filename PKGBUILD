# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=polkit
pkgver=0.98
pkgrel=1
pkgdesc="Application development toolkit for controlling system-wide privileges"
arch=(i686 x86_64)
license=('LGPL')
url="http://www.freedesktop.org/wiki/Software/PolicyKit"
depends=('glib2>=2.25.15' 'pam' 'expat>=2.0.1')
makedepends=('intltool>=0.41.1' 'gtk-doc>=1.15' 'gobject-introspection>=0.9.5')
replaces=('policykit')
options=('!libtool')
source=(http://hal.freedesktop.org/releases/${pkgname}-${pkgver}.tar.gz
        polkit-git-fixes.patch
        polkit.pam)
md5sums=('96e583a1177ba5436f034a2fee55f5fa'
         'c5aaa13d6eeda5cec224b273acba9420'
         '6564f95878297b954f0572bc1610dd15')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  patch -Np1 -i "${srcdir}/polkit-git-fixes.patch"
  libtoolize --force
  autoreconf
  ./configure --prefix=/usr --sysconfdir=/etc \
      --localstatedir=/var --libexecdir=/usr/lib/polkit-1 \
      --disable-static --enable-gtk-doc
  make
  make DESTDIR="${pkgdir}" install

  install -m644 "${srcdir}/polkit.pam" "${pkgdir}/etc/pam.d/polkit-1"
}
