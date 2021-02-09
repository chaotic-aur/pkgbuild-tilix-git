# Maintainer: Igor <f2404@yandex.ru>
# Maintainer: Davi da Silva Böger <dsboger at gmail dot com>

pkgname=tilix-git
_pkgname=tilix
pkgver=1.8.9.r33.c3fd5bfc
pkgrel=1
pkgdesc="A tiling terminal emulator for Linux using GTK+ 3 (git master)"
arch=('x86_64' 'i686')
url="https://gnunn1.github.io/tilix-web/"
license=('MPL')
depends=('libx11' 'gtkd' 'vte3' 'dconf' 'gsettings-desktop-schemas')
optdepends=('python-nautilus: for "Open Tilix Here" support in nautilus'
            'vte3-notification: for desktop notifications support'
            'vte3-tilix: for notifications, triggers and badges support'
            'libsecret: for the password manager')
makedepends=('git' 'ldc' 'po4a' 'meson')
provides=('terminix' 'tilix')
conflicts=('terminix' 'tilix')
source=('git+https://github.com/gnunn1/tilix')
sha512sums=('SKIP')

pkgver() {
  cd ${_pkgname}
  # sed transformation explained:
  # s/^v// - removes the leading "v" from the tag name, if any (tilix doesn't use it, but harmless)
  # s/\([^-]*-\)g/r\1/ - replaces the "g" that precedes the commit hash with "r"
  # s/-/./g - replaces all the remaining "-" with "."
  git describe --long --tags | sed 's/^v//;s/\([^-]*-\)g/r\1/;s/-/./g'
}

build() {
  arch-meson ${_pkgname} build
  meson -C build compile
}

package() {
  cd ${_pkgname}
  DESTDIR=${pkgdir} meson -C build install
}

