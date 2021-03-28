# Maintainer: Edward Pacman <edward at edward-p dot xyz>
# Contributer: Nick Østergaard <oe.nick at gmail dot com>

pkgname=kicad-test
pkgver=5.99.0.r10023.g8a8167ff0a
pkgrel=1
pkgdesc="Electronic schematic and printed circuit board (PCB) design tools"
arch=('i686' 'x86_64')
url="http://kicad-pcb.org/"
license=('GPL')
depends=('wxgtk3' 'python' 'desktop-file-utils' 'boost-libs' 'glew' 'curl' 'ngspice' 'opencascade' 'python-wxpython' 'doxygen' 'freetype2' 'ngspice>=27' 'swig' )
makedepends=('git' 'cmake' 'glm' 'zlib' 'mesa' 'boost' 'swig' 'ninja')
optdepends=('kicad-library: for footprints and symbols'
            'kicad-library-3d: for 3d models of components')
conflicts=('kicad' 'kicad-bzr' 'kicad-git')
provides=('kicad')
#"${pkgname}"::'https://gitlab.com/kicad/code/kicad.git'
source=("${pkgname}"::'git+https://gitlab.com/kicad/code/kicad.git'
    "kicad-test.env")
#source=("${pkgname}"::'git+https://gitlab.com/rockola/kicad.git')
md5sums=('SKIP'
        'SKIP')

pkgver() {
    cd "${srcdir}/${pkgname}"
    git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
    sed -i "s|if( !m_locale->Init( m_language_id ) )|if( !m_locale->Init( m_language_id, wxLOCALE_DONT_LOAD_DEFAULT ) )|g" "${srcdir}/${pkgname}/common/pgm_base.cpp"
}

build() {
         cd "${srcdir}/${pkgname}"
#         git switch -c test 49eb23bf 
#         git switch -c test 61ecfb1d 
#         git switch -c test 68312fb6 
#         git switch -c test 392fb298
         mkdir -p build
         cd build
  
#  -DCMAKE_BUILD_TYPE=Release
         cmake .. -G Ninja -DCMAKE_BUILD_TYPE=Debug \
        -DKICAD_STDLIB_LIGHT_DEBUG=ON \
        -DCMAKE_INSTALL_PREFIX=/usr/lib/kicad-test \
        -DCMAKE_INSTALL_DATADIR=/usr/share/kicad-test \
        -DCMAKE_INSTALL_DOCDIR=/usr/share/doc/kicad-test \
        -DCMAKE_INSTALL_LIBDIR=/usr/lib/kicad-test/lib \
        -DCMAKE_EXECUTABLE_SUFFIX=-test \
        -DKICAD_USE_OCE=OFF \
        -DKICAD_USE_OCC=ON \
        -DKICAD_BUILD_I18N=ON \
        -DBUILD_GITHUB_PLUGIN=ON \
        -DKICAD_SCRIPTING=ON \
        -DKICAD_SCRIPTING_PYTHON3=ON \
        -DKICAD_SCRIPTING_MODULES=ON \
        -DKICAD_SCRIPTING_WXPYTHON=ON \
        -DKICAD_SCRIPTING_ACTION_MENU=ON \
        -DKICAD_SCRIPTING_WXPYTHON_PHOENIX=ON \
        -DKICAD_DATA=/usr/share/kicad-test \
        -DwxWidgets_CONFIG_EXECUTABLE=/usr/bin/wx-config-gtk3
            
#         make
         ninja

#  cd "${srcdir}/${pkgname}/translation"
#  mkdir -p build
#  cd build
#  cmake .. -DCMAKE_INSTALL_PREFIX=/usr

#  make
}

package() {
  cd "${srcdir}/${pkgname}/build"
#   make DESTDIR="${pkgdir}" install
	DESTDIR="$pkgdir" ninja install
	
	mkdir -p "$pkgdir/usr/share/applications"
	for prog in bitmap2component eeschema gerbview kicad pcbcalculator pcbnew; do
		sed -i \
			-e 's/^Exec=\([^ ]*\)\(.*\)$/Exec=\1-test\2/g' \
			-e 's/^Icon=\(.*\)$/Icon=\1-test/g' \
			-e 's/^Name=\(.*\)$/Name=\1 test/g' \
			"$pkgdir/usr/share/kicad-test/applications/$prog.desktop"
		ln -sv "../kicad-test/applications/$prog.desktop" \
			"$pkgdir/usr/share/applications/${prog}-test.desktop"
	done

	cd "$srcdir"
	mkdir -p "$pkgdir/usr/share/kicad-test"
	cp kicad-test.env "$pkgdir/usr/share/kicad-test/kicad-test.env"

	mkdir -p "$pkgdir/usr/bin"
	(cd "$pkgdir/usr/lib/kicad-test/bin" && ls | grep -v '\.kiface') | while read prog; do
		cat > "$pkgdir/usr/bin/$prog-test" <<EOF
#!/bin/sh
. /usr/share/kicad-test/kicad-test.env
exec /usr/lib/kicad-test/bin/$prog
EOF
		chmod +x "$pkgdir/usr/bin/$prog-test"
	done
}
