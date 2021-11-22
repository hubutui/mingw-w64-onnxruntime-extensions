# Maintainer: Hu Butui <hot123tea123@gmail.com>

_realname=onnxruntime-extensions
pkgbase=mingw-w64-${_realname}
pkgname=("${MINGW_PACKAGE_PREFIX}-${_realname}")
pkgver=0.4.2
pkgrel=1
pkgdesc="The shared custom operator library for ONNXRuntime"
arch=('any')
mingw_arch=('mingw32' 'mingw64' 'ucrt64' 'clang64' 'clang32')
url="https://github.com/microsoft/onnxruntime-extensions"
license=('MIT')
depends=(
  "${MINGW_PACKAGE_PREFIX}-gcc-libs"
)
makedepends=("${MINGW_PACKAGE_PREFIX}-cmake")
source=("${_realname}-${pkgver}.tar.gz::https://github.com/microsoft/onnxruntime-extensions/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('f9a60112068df066ee38a97c7b06f86c2f603b9a846e02383fd30c261e6859fc')

build() {
  echo "==> Build static version"
  MSYS2_ARG_CONV_EXCL="-DCMAKE_INSTALL_PREFIX=" \
  ${MINGW_PREFIX}/bin/cmake.exe \
    -B "${srcdir}/build-static-${MINGW_CHOST}" \
    -DBUILD_SHARED_LIBS=OFF \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=${MINGW_PREFIX} \
    -DOCOS_ENABLE_CTEST=OFF \
    -DOCOS_ENABLE_PYTHON=OFF \
    -DOCOS_ENABLE_STATIC_LIB=ON \
    -G'MSYS Makefiles' \
    -S ${_realname}-${pkgver}
  ${MINGW_PREFIX}/bin/cmake.exe --build "${srcdir}/build-static-${MINGW_CHOST}"

  echo "==> Build shared version"
  MSYS2_ARG_CONV_EXCL="-DCMAKE_INSTALL_PREFIX=" \
  ${MINGW_PREFIX}/bin/cmake.exe \
    -B "${srcdir}/build-shared-${MINGW_CHOST}" \
    -DBUILD_SHARED_LIBS=ON \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=${MINGW_PREFIX} \
    -DOCOS_ENABLE_CTEST=OFF \
    -DOCOS_ENABLE_PYTHON=OFF \
    -DOCOS_ENABLE_STATIC_LIB=OFF \
    -G'MSYS Makefiles' \
    -S ${_realname}-${pkgver}
  ${MINGW_PREFIX}/bin/cmake.exe --build "${srcdir}/build-shared-${MINGW_CHOST}"
}

package() {
  DESTDIR="${pkgdir}" \
  ${MINGW_PREFIX}/bin/cmake.exe \
    --build "${srcdir}/build-static-${MINGW_CHOST}" \
    --target install

  DESTDIR="${pkgdir}" \
  ${MINGW_PREFIX}/bin/cmake.exe \
    --build "${srcdir}/build-shared-${MINGW_CHOST}" \
    --target install
}
