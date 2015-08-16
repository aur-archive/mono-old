# $Id: PKGBUILD 50106 2009-08-22 12:05:20Z daniel $
# Maintainer: Daniel Isenmann <daniel@archlinux.org>
# Contributor: Brice Carpentier <brice@dlfp.org>
# mono-242 maintainer: Zauber Exonar <zauberexonar at gmail dot com>

pkgname=mono-old
pkgver=2.4.2.3
pkgrel=1
pkgdesc="Provides mono 2.4.2 environment for opensimulator so that SQLite3 works"
arch=(i686 x86_64)
license=('GPL' 'LGPL2' 'MPL' 'custom:MITX11')
url="http://www.mono-project.com/"
depends=('zlib' 'libgdiplus>=2.4.2' 'sh')
makedepends=('pkgconfig')
options=('!libtool' '!makeflags')
replaces=('mono')
provides=('monodoc' 'mono')
conflicts=('monodoc')
source=(http://ftp.novell.com/pub/mono/sources/mono/mono-${pkgver}.tar.bz2
        mono.rc.d)
md5sums=('696f25afc8453cd0d1c78de6e905dcf2'
         '8315e46c6a6e9625502521fc0ad1a322')

build() {
  mkdir -p ${startdir}/pkg/usr/share/licenses/mono
  # build mono
  cd ${startdir}/src/mono-${pkgver}

  ./configure --prefix=/usr --sysconfdir=/etc \
              --with-libgdiplus=installed \
              --with-tls=__thread \
              --with-moonlight=yes
  make || return 1
  make DESTDIR=${startdir}/pkg install || return 1

  # install daemons and pathes
  mkdir -p ${startdir}/pkg/etc/rc.d
  install -m755 ${startdir}/src/mono.rc.d $startdir/pkg/etc/rc.d/mono

  #install license
  install -m644 mcs/MIT.X11 ${startdir}/pkg/usr/share/licenses/mono/
}
