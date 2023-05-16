# Maintainer: Bardia Moshiri <fakeshell@bardia.tech>

pkgname=qt5-qpa-hwcomposer-plugin
pkgver=5.15
pkgrel=2
arch=('aarch64')
url='https://github.com/mer-hybris/qt5-qpa-hwcomposer-plugin.git'
license=('GPL3' 'LGPL' 'custom')
pkgdesc='Qt QPA plugin for Android hwcomposer'
depends=('qt5-es2-base' 'qt5-es2-wayland' 'qt5-sensors-sensorfw' 'android-headers' 'libhybris')
makedepends=('git')
source=('qt5-qpa-hwcomposer-plugin::git+https://github.com/mer-hybris/qt5-qpa-hwcomposer-plugin.git'
        '0001-build-errors.patch'
        '0002-qeglpbuffer-include.patch')

sha256sums=('SKIP'
            'b71f8ed20b4ccf105c948eec7f7bfc9fb3a0c210bac2805cdd86866e3ee6ec8c'
            '0dc7aa8329453aaac57861ee27236c9e2b5358b5ed9734ed4c0a788e41337037')

prepare() {
  cd "${srcdir}/${pkgname}"
  mkdir -p build

  local src
  for src in "${source[@]}"; do
    src="${src%%::*}"
    src="${src##*/}"
    [[ $src = *.patch ]] || continue
    echo "Applying patch $src..."
    patch -Np1 < "../$src"
   done
}

build() {
  cd "${srcdir}/${pkgname}/build"
  qmake ../hwcomposer/
  make
}

package() {
  cd "${srcdir}/${pkgname}/build"
  make INSTALL_ROOT="$pkgdir" install
}
