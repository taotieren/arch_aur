# Maintainer: Edward Pacman <edward at edward-p dot xyz>
# Contributer: Nick Østergaard <oe.nick at gmail dot com>

pkgname=kicad-test
_langpack=kicad-i18n-test
replaces=(${_langpack})
pkgver=r20075.2d1d16d7a2
pkgrel=1
pkgdesc="Electronic schematic and printed circuit board (PCB) design tools"
arch=('i686' 'x86_64')
url="http://kicad-pcb.org/"
license=('GPL')
depends=('wxgtk3' 'python' 'boost-libs' 'glew' 'curl' 'ngspice' 'opencascade' 'python-wxpython')
makedepends=('git' 'cmake' 'glm' 'zlib' 'mesa' 'boost' 'swig')
optdepends=('kicad-library: for footprints and symbols'
            'kicad-library-3d: for 3d models of components')
conflicts=('kicad' 'kicad-bzr')
provides=('kicad')
#"${pkgname}"::'https://gitlab.com/kicad/code/kicad.git'
source=(
        "${pkgname}"::'https://gitlab.com/rockola/kicad.git'
        )
md5sums=('SKIP'
         )

#pkgver() {
# cd "${srcdir}/${pkgname}"
# printf "r%s.%s" "$(git rev-list HEAD --count --first-parent)" "$(git rev-parse --short HEAD)"
#}

build() {
# cd "${srcdir}/${pkgname}"
#git switch -c test 61ecfb1d
  git switch -c test 49eb23bf 
  mkdir -p build
  cd build
  
#  -DCMAKE_BUILD_TYPE=Release
  cmake .. -DCMAKE_BUILD_TYPE=Debug \
    -DKICAD_STDLIB_LIGHT_DEBUG=ON \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=lib \
    -DKICAD_USE_OCE=OFF \
    -DKICAD_USE_OCC=ON \
    -DKICAD_BUILD_I18N=ON \
    -DBUILD_GITHUB_PLUGIN=ON \
    -DKICAD_SCRIPTING=ON \
    -DKICAD_SCRIPTING_MODULES=ON \
    -DKICAD_SCRIPTING_ACTION_MENU=ON \
    -DKICAD_SCRIPTING_PYTHON3=ON \
    -DKICAD_SCRIPTING_WXPYTHON=ON \
    -DwxWidgets_CONFIG_EXECUTABLE=/usr/bin/wx-config-gtk3 \
    -DKICAD_SCRIPTING_WXPYTHON_PHOENIX=ON

  make

#  cd "${srcdir}/${pkgname}/translation"
#  mkdir -p build
#  cd build
#  cmake .. -DCMAKE_INSTALL_PREFIX=/usr

#  make
}

package() {
  cd "${srcdir}/${pkgname}"
  cd build
  make DESTDIR="${pkgdir}" install
}
