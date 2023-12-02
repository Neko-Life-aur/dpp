# Maintainer: Neko-Life <nekolife123579 at gmail dot com>
# See also https://github.com/Neko-Life-aur/dpp
#
# Contributor: Jakub 'Eremiell' Marek <eremiell at eremiell dot net>
# See also https://github.com/eremiell-aur/dpp
pkgname=dpp
_pkgname=DPP
pkgver=10.0.27
pkgrel=1
pkgdesc="Lightweight and Scalable C++ Discord API Bot Library"
arch=('x86_64')
url="https://dpp.dev/"
_url="https://github.com/brainboxdotcc/${_pkgname}"
license=('Apache')
depends=('glibc' 'gcc-libs' 'openssl' 'zlib' 'nlohmann-json')
makedepends=('cmake' 'pkgconf')
optdepends=('opus: voice support'
            'libsodium: voice support')
install="${pkgname}.install"
changelog="${pkgname}.changelog"
source=("${_url}/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('525a5c10a5fdd69996f48826ea1c37a3f08ba934c95e4cb9738afd209a2ecdb7')
validpgpkeys=('EDCEFB1FDAFFAC7952EED46F9927644B850BDD23')

prepare() {
	cd "${srcdir}/${_pkgname}-${pkgver}"
	rm -rf "include/dpp/nlohmann"
	#sed -i -E "s/(#pragma once)/\1\n#include <cstdint>/" "include/dpp/sslclient.h"
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
