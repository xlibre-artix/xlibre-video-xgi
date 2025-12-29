# Maintainer: artist for Artix Linux and XLibre <artist@artixlinux.org>

pkgname=xlibre-video-xgi
pkgver=25.0.0
pkgrel=4
pkgdesc="XLibre fork of xgi video driver"
arch=(x86_64)
license=('X11')
_pkgname="${pkgname//xlibre/xf86}"
url="https://github.com/X11Libre/${_pkgname}"
depends=("xlibre-xserver>=${pkgver%.*}" 'glibc')
makedepends=("xlibre-xserver-devel>=${pkgver%.*}" 'xorgproto')
conflicts=("${_pkgname}")
provides=("${_pkgname}")
source=("${url}/archive/refs/tags/xlibre-${_pkgname}-${pkgver}.tar.gz")
groups=('xlibre-drivers')

build() {
  cd ${_pkgname}-xlibre-${_pkgname}-${pkgver}
  export CFLAGS=${CFLAGS/-fno-plt}
  export CXXFLAGS=${CXXFLAGS/-fno-plt}
  export LDFLAGS=${LDFLAGS/-Wl,-z,now}
export CFLAGS+=" -std=gnu17"
export CFLAGS+=" -Wno-error=incompatible-pointer-types -Wno-int-conversion"

  ./autogen.sh
  ./configure --prefix=/usr
  make
}

check() {
  cd ${_pkgname}-xlibre-${_pkgname}-${pkgver}
  make check
}

package() {
  cd ${_pkgname}-xlibre-${_pkgname}-${pkgver}
  make DESTDIR="${pkgdir}" install
  install -Dm644 "${srcdir}"/${_pkgname}-xlibre-${_pkgname}-${pkgver}/COPYING "${pkgdir}"/usr/share/licenses/${pkgname}/LICENSE
}

sha256sums=('7d634a13618b6ccee793d61d96c1db7ac18212433e4793697f62a101fb3ef5ed')
