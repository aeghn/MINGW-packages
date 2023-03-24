# Maintainer: Alberto Fanjul Alonso <albfan@gnome.org>

_realname=minder-git
pkgbase=mingw-w64-${_realname}
pkgname="${MINGW_PACKAGE_PREFIX}-${_realname}"
pkgver=0.9999.0
pkgrel=1
arch=('any')
mingw_arch=('clang64')
pkgdesc="Mind-mapping application designed for Pantheon"
depends=( "${MINGW_PACKAGE_PREFIX}-granite"
          "${MINGW_PACKAGE_PREFIX}-elementary-icon-theme"
          "${MINGW_PACKAGE_PREFIX}-gtk-elementary-theme"
          "${MINGW_PACKAGE_PREFIX}-libarchive"
          "${MINGW_PACKAGE_PREFIX}-goocanvas"
          "${MINGW_PACKAGE_PREFIX}-gtk3"
          "${MINGW_PACKAGE_PREFIX}-cairo"
          "${MINGW_PACKAGE_PREFIX}-discount"
          "${MINGW_PACKAGE_PREFIX}-glib2"
          "${MINGW_PACKAGE_PREFIX}-gtksourceview4"
          "${MINGW_PACKAGE_PREFIX}-libarchive"
          "${MINGW_PACKAGE_PREFIX}-libgee"
          "${MINGW_PACKAGE_PREFIX}-gsettings-desktop-schemas"
          "${MINGW_PACKAGE_PREFIX}-libxml2")
makedepends=("${MINGW_PACKAGE_PREFIX}-meson"
             "${MINGW_PACKAGE_PREFIX}-pkg-config"
             "${MINGW_PACKAGE_PREFIX}-vala"
             "${MINGW_PACKAGE_PREFIX}-cc"
             "${MINGW_PACKAGE_PREFIX}-gobject-introspection"
             "${MINGW_PACKAGE_PREFIX}-itstool"
             "${MINGW_PACKAGE_PREFIX}-libhandy"
             "git"
             "${MINGW_PACKAGE_PREFIX}-meson"
             "${MINGW_PACKAGE_PREFIX}-ninja")
options=('strip')
license=("GPL3")
url="https://github.com/phase1geo/Minder"
source=("${_realname}-${pkgver}::git+https://github.com/phase1geo/Minder.git"
        Patch-for-widnows-build.patch)
sha256sums=('SKIP'
            'SKIP')

prepare() {
  cd "${srcdir}/${_realname}-${pkgver}"
  patch -N -p1 -i "${srcdir}/Patch-for-widnows-build.patch"
}

build() {
  [[ -d build-${MINGW_CHOST} ]] && rm -rf build-${MINGW_CHOST}
  mkdir -p build-${MINGW_CHOST}
  cd build-${MINGW_CHOST}

  MSYS2_ARG_CONV_EXCL="--prefix=" \
  meson \
    --prefix="${MINGW_PREFIX}" \
    --buildtype plain \
    -Dwerror=false \
    ../${_realname}-${pkgver}

  meson compile
}

package() {
  cd "${srcdir}/build-${MINGW_CHOST}"
  DESTDIR="${pkgdir}" meson install

  install -Dm644 "${srcdir}/${_realname}-${pkgver}/COPYING" "${pkgdir}${MINGW_PREFIX}/share/licenses/${_realname}/COPYING"
}
