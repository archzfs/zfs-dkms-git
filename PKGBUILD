# Maintainer: Jan Houben <jan@nexttrex.de>
# Contributor: Jesus Alvarez <jeezusjr at gmail dot com>
#
# This PKGBUILD was generated by the archzfs build scripts located at
#
# http://github.com/archzfs/archzfs
#
pkgname="zfs-dkms-git"
_commit='7fcf82451c4b75afe327c77683f66bf0c6396a48'
pkgdesc="Kernel modules for the Zettabyte File System."

pkgver=2020.05.10.r5897.g7fcf82451
pkgrel=1
makedepends=("git")
arch=("x86_64")
url="https://zfsonlinux.org/"
source=("git+https://github.com/zfsonlinux/zfs.git#commit=${_commit}"
        "linux-5.5-compat-blkg_tryget.patch"
        "linux-5.6-compat-struct-proc_ops.patch"
        "linux-5.6-compat-timestamp_truncate.patch"
        "linux-5.6-compat-ktime_get_raw_ts64.patch"
        "linux-5.6-compat-time_t.patch")
sha256sums=("SKIP"
            "daae58460243c45c2c7505b1d88dcb299ea7d92bcf3f41d2d30bc213000bb1da"
            "05ca889a89b1e57d55c1b7d4d3013398a3e5a69d0fad27278aad701f0bb6e802"
            "5ad4393b334a8f685212f47b44e98dc468c70214ee5dbbab24cc95c4f310ae39"
            "7c6ebee72d864160b376fc18017c81f499f177b7d9265f565de859139805a277"
            "06f7ade5adcbfe77cb234361f8b2aca6d6e78fcd136da6d3a70048b5e92c62bb")
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
