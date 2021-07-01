# Maintainer: Jan Houben <jan@nexttrex.de>
# Contributor: Jesus Alvarez <jeezusjr at gmail dot com>
#
# This PKGBUILD was generated by the archzfs build scripts located at
#
# http://github.com/archzfs/archzfs
#
pkgname="zfs-dkms-rc"
pkgdesc="Kernel modules for the Zettabyte File System."

pkgver=2.1.0_rc8
pkgrel=1
makedepends=()
arch=("x86_64")
url="https://zfsonlinux.org/"
source=("https://github.com/zfsonlinux/zfs/releases/download/zfs-${pkgver/_/-}/zfs-${pkgver/_/-}.tar.gz")
sha256sums=("8627702ac841d38d5211001c76937e4097719c268b110e8836c0da195618fad2")
license=("CDDL")
depends=("zfs-utils-rc=${pkgver}" "lsb-release" "dkms")
provides=("zfs" "zfs-headers" "spl" "spl-headers")
groups=("archzfs-dkms-rc")
conflicts=("zfs" "zfs-headers" "spl" "spl-headers")

build() {
    cd "${srcdir}/zfs-${pkgver/_rc*/}"
    ./autogen.sh
}

package() {
    dkmsdir="${pkgdir}/usr/src/zfs-${pkgver}"
    install -d "${dkmsdir}"
    cp -a ${srcdir}/zfs-${pkgver/_rc*/}/. ${dkmsdir}
    cd "${dkmsdir}"
    find . -name ".git*" -print0 | xargs -0 rm -fr --
    scripts/dkms.mkconf -v ${pkgver} -f dkms.conf -n zfs
    chmod g-w,o-w -R .
}
