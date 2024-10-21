# Maintainer: Neko-Life <nekolife123579 at gmail dot com>
# See also https://github.com/Neko-Life-aur/dpp
#
# Contributor: Jakub 'Eremiell' Marek <eremiell at eremiell dot net>
# See also https://github.com/eremiell-aur/dpp
pkgname=dpp
_pkgname=DPP
pkgver=10.0.33
pkgrel=1
pkgdesc="Lightweight and Scalable C++ Discord API Bot Library"
arch=('x86_64')
url="https://dpp.dev/"
_url="https://github.com/brainboxdotcc/${_pkgname}"
license=('Apache')
depends=('glibc' 'gcc-libs' 'openssl' 'zlib' 'nlohmann-json')
makedepends=('cmake' 'pkgconf')
optdepends=('opus: voice support')
install="${pkgname}.install"
changelog="${pkgname}.changelog"
source=("${_url}/releases/download/v${pkgver}/${_pkgname}-${pkgver}.tar.gz"
	"${_url}/releases/download/v${pkgver}/${_pkgname}-${pkgver}.tar.gz.asc")
sha256sums=('75ee7b32c9d46bde6d02b46b3a907302865a4ee4a965ef8a575b7417bb0a46fe'
            'SKIP')
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
	ln -s "/usr/include/nlohmann" "${pkgdir}/usr/include/dpp/nlohmann"
}
