# Maintainer: Jan Houben <jan@nexttrex.de>
# Contributor: Jesus Alvarez <jeezusjr at gmail dot com>
#
# This PKGBUILD was generated by the archzfs build scripts located at
#
# http://github.com/archzfs/archzfs
#
pkgname="zfs-dkms-git"
_commit='9305ff2edf7ff67cdd2cc3d38884fa4f5de6dadd'
pkgdesc="Kernel modules for the Zettabyte File System."

pkgver=2021.03.12.r6623.g9305ff2ed
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
    chmod g-w,o-w -R .
}
