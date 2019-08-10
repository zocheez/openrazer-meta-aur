# Maintainer: Luca Weiss <luca (at) z3ntu (dot) xyz>
# Contributor: Gabriele Musco <emaildigabry@gmail.com>

pkgbase=openrazer
pkgname=('python-openrazer' 'openrazer-daemon' 'openrazer-driver-dkms' 'openrazer-meta')
pkgver=2.6.0
pkgrel=1
pkgdesc="An entirely open source driver and user-space daemon that allows you to manage your Razer peripherals on GNU/Linux."
arch=('any')
url="https://github.com/openrazer/openrazer"
license=('GPL2')
makedepends=('python-setuptools')
source=("https://github.com/trialism/openrazer/archive/master.zip")
sha256sums=('35d4134fb5ecfbb35822cb8ffd7ab25ab06eb54480aa13dcb0c03c75a1caed22')

package_python-openrazer() {
  pkgdesc="Python library for accessing the Razer daemon from Python."
  depends=('openrazer-daemon' 'python-numpy')

  cd "openrazer-master"
  make DESTDIR="$pkgdir" python_library_install
}

package_openrazer-daemon() {
  pkgdesc="Userspace daemon that abstracts access to the kernel driver. Provides a DBus service for applications to use."
  depends=('openrazer-driver-dkms' 'gtk3' 'python-dbus' 'python-gobject' 'python-setproctitle' 'python-daemonize' 'python-notify2' 'python-pyudev')
  install=openrazer-daemon.install

  cd "openrazer-master"
  make DESTDIR="$pkgdir" daemon_install
}

package_openrazer-driver-dkms() {
  pkgdesc="Kernel driver for Razer devices (DKMS-variant)"
  depends=('dkms' 'udev')
  install=openrazer-driver-dkms.install

  cd "openrazer-master"
  make DESTDIR="$pkgdir" setup_dkms udev_install
}

package_openrazer-meta() {
  pkgdesc="Meta package for installing all required openrazer packages."
  depends=('openrazer-driver-dkms' 'openrazer-daemon' 'python-openrazer')
  optdepends=('polychromatic: frontend'
              'razergenie: qt frontend'
              'razercommander: gtk frontend')
}
