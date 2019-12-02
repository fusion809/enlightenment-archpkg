# Maintainer: Ronald van Haren <ronald@archlinux.org>
# Contributor: Enlightenment Developers <enlightenment-devel@enlightenment.org>>

pkgname=enlightenment
pkgver=0.23.1
pkgrel=1
pkgdesc="Enlightenment window manager"
arch=('x86_64')
url="http://www.enlightenment.org"
license=('BSD')
depends=('efl' 'xcb-util-keysyms' 'hicolor-icon-theme' 'pixman' 'mesa'
         'desktop-file-utils' 'udisks2' 'ttf-font' 'bluez-libs' 'pam')
optdepends=('connman: network module'
            'acpid: power events on laptop lid close'
	        'geoip-database: geolocation module'
            'xorg-server-xwayland: xwayland support')
makedepends=('xorg-server-xwayland')
provides=('notification-daemon')
backup=('etc/enlightenment/sysactions.conf'
        'etc/xdg/menus/e-applications.menu')
source=("https://download.enlightenment.org/rel/apps/${pkgname}/$pkgname-$pkgver.tar.xz")
sha256sums=('e530590c09b560679621f4531d55c242cfafe8523309e0ae88fb267e00f52c34')


build() {
  cd "${srcdir}/${pkgname}-${pkgver}"

  export CFLAGS="$CFLAGS -fvisibility=hidden"

  rm -rf build
  meson --prefix=/usr \
    -Dwl=true \
    . build

  ninja -C build
}


package() {
  cd "${srcdir}/${pkgname}-${pkgver}"

  DESTDIR="$pkgdir" ninja -C build install

  # install LICENSE
  install -Dm644 COPYING "$pkgdir/usr/share/licenses/$pkgname/COPYING"
}
