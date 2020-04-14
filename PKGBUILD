# $Id$
# Maintainer: TheKit <nekit1000 at gmail.com>
# Maintainer: James Kittsmiller (AJSlye) <james@nulogicsystems.com>

pkgname=qt5-around-git
_pkgname=qtaround-git
pkgver=0.2.10.r0.ga1722f7
pkgrel=1
pkgdesc="QtAround library used to port the-vault to C++"
arch=('x86_64' 'aarch64')
url="https://git.sailfishos.org/mer-core/qtaround"
license=('GPL')
depends=('qt5-base')
makedepends=('git' 'cor' 'tut')
provides=("${pkgname%-git}" "${_pkgname%-git}")
conflicts=("${pkgname%-git}" "${_pkgname%-git}")
source=('git+https://git.sailfishos.org/mer-core/qtaround.git')
md5sums=('SKIP')

pkgver() {
	cd "$srcdir/${_pkgname%-git}"
	git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
	cd "$srcdir/${_pkgname%-git}"
    sed -i "s|tut>=0.0.3|tut>=0.0.0|g" ./tests/CMakeLists.txt
    sed -i "s|#include <QMap>|#include <QMap>\n#include <cmath>|g" ./src/util.cpp
}

build() {
	cd "$srcdir/${_pkgname%-git}"
	cmake -DCMAKE_INSTALL_PREFIX=/usr -DVERSION=$pkgver
	make
}

package() {
	cd "$srcdir/${_pkgname%-git}"
	make DESTDIR="$pkgdir/" install
}
