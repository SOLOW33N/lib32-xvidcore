#!/bin/bash

# Created from the original package by

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# [ToDo]: Add files: User documentation
# [ToDo]: Add files: Tooling
# [FixMe]: Namcap warnings and errors


# Maintainer: Nocifer <apmichalopoulos at gmail dot com>
# Contributor: Tod Jackson <tod.jackson@gmail.com>
# Contributor: tobias <tobias@archlinux.org>
# Contributor: Sarah Hay <sarah@archlinux.org>
# Contributor: JD Steffen <jd@steffennet.org>
# Contributor: GordonGR <ntheo1979@gmail.com>



_relname=xvidcore
pkgname=lib32-$_relname
pkgver=1.3.7
pkgrel=2
pkgdesc="XviD is an open source MPEG-4 video codec (32-bit)"
arch=("x86_64")
url="https://www.xvid.com"
license=("GPL")
depends=(
    "$_relname"
     "lib32-glibc"
     )
makedepends=(
    "nasm" 
    "lib32-gcc-libs"
    )
provides=(
    "libxvidcore.so"
    )
source=(
    "https://downloads.xvid.com/downloads/${_relname}-${pkgver}.tar.gz"
    )
sha512sums=(
    "b66b1b0c9ddf4cc48fddd3afc1a8382b21e8bc7dc8a50220bcf1a86e6a2dab9abdcbd3dc64e27a054087f6770a4731468c301351d166c1a19e7f419b04ba7b9b"
    )

build() {
    cd ${srcdir}/${_relname}/build/generic

    export CC="gcc -m32"
    export CXX="g++ -m32"
    export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"

    ./configure --prefix=/usr \
                --libdir=/usr/lib32 \
                --host=x86_64-unknown-linux-gnu \
                --target=i686-unknown-linux-gnu
    make
}

package() {
    cd ${srcdir}/${_relname}/build/generic

    make DESTDIR=${pkgdir} install
    rm -rf "${pkgdir}"/usr/{include,share,bin}

    #Fix dynamic libraries
    cd ${pkgdir}/usr/lib32
    ln -sf libxvidcore.so.4.3 libxvidcore.so.4
    ln -sf libxvidcore.so.4.3 libxvidcore.so
}
