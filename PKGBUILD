pkgname=mm-common
pkgver=1.0.7
pkgrel=2
pkgdesc="Common build files of the C++ bindings"
arch=('x86_64')
url="https://gtkmm.gnome.org/"
license=('GPL-2.0-or-later')
depends=(
    'bash'
    'perl-xml-parser'
    'python'
)
makedepends=(
    'git'
    'libsigc++'
    'meson'
)
_docver=15.1.0
_docurl=https://gcc.gnu.org/onlinedocs/gcc-${_docver}/libstdc++/api/
source=(git+https://gitlab.gnome.org/GNOME/mm-common.git#tag=${pkgver}
    libstdc++-${_docver}.tag::${_docurl}libstdc++.tag)
sha256sums=(8e73815316dbd74d01e18828f619bce303e0e999e0045225a493bcacd73e538c
    f95a2cc3959b6d96e2dceb396479a80c04f886c969c2ad34e614d8cbdf6f0e9d)

prepare() {
    cd ${pkgname}

    # Use more stable libstdc++ tags
    cp ${srcdir}/libstdc++-${_docver}.tag doctags/libstdc++.tag

    local f; git grep -lz latest-doxygen | while read -r -d '' f; do
        sed -ri 's|https?://gcc\.gnu\.org/onlinedocs/libstdc\+\+/latest-doxygen/|'"${_docurl}"'|g' ${f}
    done
}

build() {
    cd ${pkgname}

    local meson_args=(
    )

    ${meson_options} "${meson_args[@]}"

    ${meson_build}
}

package() {
    cd ${pkgname}

    ${meson_install} ${pkgdir}
}
