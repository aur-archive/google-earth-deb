# Maintainer: Kiodo1981 <cristianmartina1981@gmail.com>

# Thanks to: 458italia <svenskaparadox@gmail.com> - Madek <gonzaloseguel@gmail.com> - Berseker <berseker86@gmail.com> - Det <nimetonmaili@gmail.com>

pkgname=google-earth-deb
pkgver=6.1.0.5001
pkgrel=1
pkgdesc="A 3D interface to view satellite images of Earth and others objects (i686 and x86_64 support)"
url="http://www.google.com/earth/index.html"
license=('custom')
arch=('i686' 'x86_64')
install=googleearth.install

[ $CARCH = 'i686' ] && _a="i386"  
depends=('libsm' 'libxrender' 'libgl' 'glib2' 'libxi' 'pcre' 'fontconfig' 'libxdamage' 'ld-lsb')
optdepends=('ttf-bitstream-vera: Fonts'
            'nss-mdns: In case the application fails to contact the servers'
            'gtk2: SCIM support'
            'nvidia-utils: 3D support for Nvidia cards'
            'catalyst-utils: 3D support for ATI/AMD cards')

source=(http://dl.google.com/dl/earth/client/current/google-earth-stable_current_i386.deb
	http://earth.google.com/intl/en/license.html
	googleearth-i686
	googleearth-x86_64
	googleearth.desktop
	googleearth-mimetypes.xml
	googleearth-icon.png
	pangorc
	qt.conf)

md5sums=('5ea7dfb007ab1c0b70038762f65081ef'
	 '7363c6144ebb298b1d7aec713ca8a82a'
	 'b955ff71ae2ad0324ff6dd22452ee32c'
	 'c96486b18f4a264a4de98c7bd4443335'
	 'cf6cf51e4a3f6d95fb743fa35db3272d'
	 'e3c67b8d05c3de50535bd7e45eee728e'
	 '0a5da8bc60fe8fe1e4641243f8e218fa'
	 'bd9f74c28489eb79f31e84977e3cf305'
	 '335088571a7182988280643c61e0230e')


[ $CARCH = 'x86_64' ] && _a="amd64"
depends=('lib32-libsm' 'lib32-libxrender' 'lib32-libgl' 'lib32-glib2' 'lib32-libxi' 'lib32-pcre' 'lib32-fontconfig' 'lib32-libxdamage' 'lib32-gcc-libs' 'ld-lsb')
optdepends=('ttf-bitstream-vera: Fonts'
            'lib32-nss-mdns: In case the application fails to contact the servers'
            'lib32-gtk2: SCIM support'
	    'lib32-nvidia-utils: 3D support for Nvidia cards'
            'lib32-catalyst-utils: 3D support for ATI/AMD cards')

source=(http://dl.google.com/dl/earth/client/current/google-earth-stable_current_amd64.deb
	http://earth.google.com/intl/en/license.html
	googleearth-i686
	googleearth-x86_64
	googleearth.desktop
	googleearth-mimetypes.xml
	googleearth-icon.png
	pangorc
	qt.conf)

md5sums=('9f010b1676c3f2938529ea08227b7694'
	 '7363c6144ebb298b1d7aec713ca8a82a'
	 'b955ff71ae2ad0324ff6dd22452ee32c'
	 'c96486b18f4a264a4de98c7bd4443335'
	 'cf6cf51e4a3f6d95fb743fa35db3272d'
	 'e3c67b8d05c3de50535bd7e45eee728e'
	 '0a5da8bc60fe8fe1e4641243f8e218fa'
	 'bd9f74c28489eb79f31e84977e3cf305'
	 '335088571a7182988280643c61e0230e')


conflicts=('google-earth' 'bin32-google-earth')

[[ "${CARCH}" == "i686" ]] && [[ "${_use_system_libs}" == "yes" ]] && depends+=('curl' 'mesa' 'qt')
[[ "${CARCH}" == "x86_64" ]] && [[ "${_use_system_libs}" == "yes" ]] && depends+=('lib32-curl' 'lib32-mesa' 'lib32-qt')

build() {
 cd $srcdir || return 1
 ar -x google-earth-stable_current_$_a.deb || return 1
 cd $pkgdir || return 1
 tar -xvf ${srcdir}/data.tar.lzma || return 1
}

package() {
  # Install the .desktop file
  install -Dm644 googleearth.desktop "${pkgdir}/usr/share/applications/googleearth.desktop"

  # Install the shared MIME info package
  install -Dm644 googleearth-mimetypes.xml "${pkgdir}/usr/share/mime/packages/googleearth-mimetypes.xml"

  # Install the icon
  install -Dm644 googleearth-icon.png "${pkgdir}/usr/share/pixmaps/googleearth-icon.png"
  
  # Install the pango config file
  [[ "${CARCH}" == "x86_64" ]] && install -Dm644 pangorc "${pkgdir}/opt/${pkgname}/pangorc"

  if [[ "${CARCH}" == "x86_64" ]] && [[ "${_use_system_libs}" == "yes" ]]; then
  	# Removing the provided libraries to use the system ones instead
  	cd "${pkgdir}/opt/${pkgname}"
  	rm ${_libs_to_remove}
  	install -Dm644 "${srcdir}/qt.conf" qt.conf
  fi

  # Change the ownership to root
  chown -R root:root ${pkgdir}/*
}
