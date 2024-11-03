# Maintainer: Neko-Life <nekolife123579 at gmail dot com>
# See also https://github.com/Neko-Life-aur/dpp
#
# Contributor: Jakub 'Eremiell' Marek <eremiell at eremiell dot net>
# See also https://github.com/eremiell-aur/dpp
pkgname=dpp
_pkgname=DPP
pkgver=10.0.35
pkgrel=1
pkgdesc="Lightweight and Scalable C++ Discord API Bot Library"
arch=('x86_64')
url="https://dpp.dev/"
_url="https://github.com/brainboxdotcc/${_pkgname}"
license=('Apache')
depends=('glibc' 'gcc-libs' 'openssl' 'zlib' 'nlohmann-json')
makedepends=('cmake' 'pkgconf')
optdepends=('opus: voice support')
changelog="${pkgname}.changelog"
source=("${_url}/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('46efde92ec6aba7f3e2b7ad17af2ffa4a18fc0bf3b3566a03f7131784ff7fdc8')
validpgpkeys=('EDCEFB1FDAFFAC7952EED46F9927644B850BDD23')

prepare() {
	cd "${srcdir}/${_pkgname}-${pkgver}"
	rm -rf "include/dpp/nlohmann"
	sed -i 's/<dpp\/nlohmann\/json.hpp>/<nlohmann\/json.hpp>/' include/dpp/json.h # temporary fix for bugged cmake
}

build() {
	cd "${srcdir}/${_pkgname}-${pkgver}"
	mkdir -p build
	cd build
	cmake -DDPP_BUILD_TEST=OFF -DRUN_LDCONFIG=OFF -DDPP_NO_VCPKG=ON -DDPP_CORO=ON -DDPP_USE_EXTERNAL_JSON=ON -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_INSTALL_MESSAGE=NEVER -Wno-dev ..
	make
}

package() {
	cd "${srcdir}/${_pkgname}-${pkgver}/build"
	make DESTDIR="${pkgdir}/" install
}
