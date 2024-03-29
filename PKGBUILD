# Maintainer: Jan Houben <jan@nexttrex.de>
# Contributor: Jesus Alvarez <jeezusjr at gmail dot com>
#
# This PKGBUILD was generated by the archzfs build scripts located at
#
# http://github.com/archzfs/archzfs
#
pkgname="zfs-dkms-git"
_commit='8f2f6cd2ac688916adb2caf979daf95365ccb48f'
pkgdesc="Kernel modules for the Zettabyte File System."

pkgver=2024.02.26.r9034.g8f2f6cd2ac
pkgrel=1
makedepends=("git")
arch=("x86_64")
url="https://openzfs.org/"
source=("git+https://github.com/openzfs/zfs.git#commit=${_commit}" "enforce-kernel-max-version.patch" "linux-6.8-compat.patch" "kernel-6.8-meta.patch")
sha256sums=("SKIP" "c5a9f546638c706844d5aff99f40366db1684679c3318d3a4093e0746748a711" "b875c877069a4c75c7b2b4b22d048e66f415b86f862ef6b3b83d3524694cc973" "1bc3b2e79e481b1bf41e78f9d142de8e97326288ecdc97f8db65496b7c4fd63b")
license=("CDDL")
depends=("zfs-utils-git=${pkgver}" "lsb-release" "dkms")
provides=("zfs" "zfs-headers" "spl" "spl-headers")
groups=("archzfs-dkms-git")
conflicts=("zfs" "zfs-headers" "spl" "spl-headers")
replaces=("spl-dkms-git")
prepare() {
    cd "${srcdir}/zfs"
    patch -Np1 -i ${srcdir}/enforce-kernel-max-version.patch
    patch -Np1 -i ${srcdir}/linux-6.8-compat.patch
    patch -Np1 -i ${srcdir}/kernel-6.8-meta.patch
}

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
