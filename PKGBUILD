# Contributor: chenxing <cxcxcxcx AT gmail DOT com>
# Contributor: Michael Burkhard <Michael DOT Burkhard AT web DOT de>
# Maintainer: alexmo82 <25396682 AT live DOT it>

pkgname=freefilesync
pkgver=7.9
pkgrel=0
pkgdesc="Backup software to synchronize files and folders"
arch=('i686' 'x86_64')
url="http://www.freefilesync.org/"
license=('GPLv3')
depends=(wxgtk webkitgtk2 boost-libs)
makedepends=(boost)
source=("http://downloads.sourceforge.net/project/zenxml/zenXml_2.3.zip"	#zen
	"FreeFileSync_${pkgver}_Source.zip::https://db.tt/ZRH1jEx3"		#ffs
#	"http://www.freefilesync.org/download/2o5osm21vcjbobv/FreeFileSync_7.9_Source.zip"
	FreeFileSync.desktop
	ffsicon.png
	RealtimeSync.desktop
	rtsicon.png)
md5sums=('58baf96cb8e1136d10e1ada7419921c5'	#zen
         'ba5f9f8f9ec70ed769ab4b3ae41f2f99'	#ffs
         'eab0ccfc6a88e229a0f07507b93cfcff'
         '1f452dff6f970d95839411008d86250b'
         'cde50b36d7b55c51ab69d5e41cd80a1f'
         'ee5587fa0a8d906ad416564e4daf5a06')

build() {
  echo -n "compiled with  "
  g++ --version		# just in case of compile errors

  cd ${srcdir}/zen
  sed -i 's/))),/) || (__GNUC_MINOR__ == 3 \&\& __GNUC_PATCHLEVEL__ < 1) )),/1' scope_guard.h

  cd ${srcdir}/FreeFileSync/Source
  sed -i 's/Sync_Complete.wav/*.wav/' Makefile
  cd ../Build
  cd ../Source
  make launchpad

  cd RealTimeSync
  make launchpad
}

package() {
  cd ${srcdir}/FreeFileSync/Source
  make DESTDIR=${pkgdir} install

  cd RealTimeSync
  make DESTDIR=${pkgdir} install

  cd ${srcdir}
  install -Dm644 FreeFileSync.desktop $pkgdir/usr/share/applications/FreeFileSync.desktop
  install -Dm644 ffsicon.png $pkgdir/usr/share/pixmaps/ffsicon.png
  install -Dm644 RealtimeSync.desktop $pkgdir/usr/share/applications/RealtimeSync.desktop
  install -Dm644 rtsicon.png $pkgdir/usr/share/pixmaps/rtsicon.png
}
