# Maintainer: Jan Houben <jan@nexttrex.de>
# Contributor: Jesus Alvarez <jeezusjr at gmail dot com>
#
# This PKGBUILD was generated by the archzfs build scripts located at
#
# http://github.com/archzfs/archzfs
#
pkgname="zfs-dkms-git"
_commit='e79b6807b8a9839dd3ced71376dc143e24949fb1'
pkgdesc="Kernel modules for the Zettabyte File System."

pkgver=2021.11.03.r7159.ge79b6807b8
pkgrel=1
makedepends=("git")
arch=("x86_64")
url="https://zfsonlinux.org/"
source=("git+https://github.com/zfsonlinux/zfs.git#commit=${_commit}")
sha256sums=("SKIP")
license=("CDDL")
depends=("zfs-utils-git=${pkgver}" "lsb-release" "dkms")
provides=("zfs" "zfs-headers" "spl" "spl-headers")
groups=("archzfs-dkms-git")
conflicts=("zfs" "zfs-headers" "spl" "spl-headers")
replaces=("spl-dkms-git")

build() {
    cd "${srcdir}/zfs"
    ./autogen.sh
}

package() {
    dkmsdir="${pkgdir}/usr/src/zfs-git"
    install -d "${dkmsdir}"
    cp -a ${srcdir}/zfs/. ${dkmsdir}
    cd "${dkmsdir}"
    find . -name ".git*" -print0 | xargs -0 rm -fr --
    scripts/dkms.mkconf -v git -f dkms.conf -n zfs
}
