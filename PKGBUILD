# Maintainer: Filipe Laíns (FFY00) <lains@archlinux.org>

pkgname=libratbag
pkgver=0.20
pkgrel=2
pkgdesc='A DBus daemon to configure gaming mice'
arch=('x86_64')
url='https://github.com/MOVZX/libratbag'
license=('MIT')
depends=('glib2' 'libevdev' 'libudev.so' 'libunistring' 'json-glib' 'python' 'python-evdev' 'python-gobject')
optdepends=('linux: Linux 5.2 is required for Logitech wireless devices')
makedepends=('meson' 'swig' 'git' 'python-sphinx' 'python-sphinx_rtd_theme' 'systemd')
checkdepends=('check' 'valgrind' 'python-gobject' 'python-lxml')
source=("git+$url")
sha512sums=('SKIP')
provides=('ratbagd' 'liblur')
conflicts=('ratbagd' 'liblur')
options=(!debug !lto strip)

build() {
  mkdir -p $pkgname/build

  cd $pkgname/build

  arch-meson .. \
  	-Dsystemd-unit-dir=/usr/lib/systemd/system \
  	-Ddocumentation=true

  ninja
}

check() {
  cd $pkgname/build

  meson test --no-rebuild
}

package() {
  cd $pkgname/build

  DESTDIR="$pkgdir" ninja install

  # Install documentation
  install -dm 755 "$pkgdir"/usr/share/doc/$pkgname
  cp -r -a --no-preserve=ownership doc/html "$pkgdir"/usr/share/doc/$pkgname
  rm -rf "$pkgdir"/usr/share/doc/$pkgname/html/.doctrees

  # Install license
  install -Dm 644 ../COPYING "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
