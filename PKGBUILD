# Maintainer: mirandir <mirandir@orange.fr>

pkgname=heebo-git
_realname=heebo
pkgver=8c21e7e
pkgrel=3
pkgdesc="Heebo is an adaptation of the classic Match-3 genre puzzle game. Align the quirky Heebos into lines of three or more. Simple but highly addictive!"
arch=('i686' 'x86_64')
url=('http://saz.im/software/heebo.html')
license=('GPL')
depends=('qt4')
makedepends=('git')
source=('heebo.desktop'
        'mainpage.patch'
        'about.html'
        'help.html'
        'map.dat'
        heebo::git+git://gitorious.org/heebo/heebo.git)
sha256sums=('8500b87c54c14de980c0c1bc8fab102af8ddcd1f8344de448d1ebdf147c9c921'
            '677fe8bfcf520640746d029ba43257b15c81d6238a39c7359a6b760670368742'
            '92e9dbd860d92f7f07ac164a46c2bc7025cdfb7185dfa7593cc1f7c86bbc11e4'
            '122d01c38c69f8d9424f14209ce1eb777e62fee14a7cb014eb9230dcb9ed3825'
            '6cb5f06acf1b1e5ab902d33f1588a168e30d17d48df00cff4367d6b8d86651a8'
            'SKIP')

pkgver() {
  cd "${srcdir}/${_realname}"
  git describe --always | sed 's|-|.|g'
}

build() {
  cd $srcdir/$_realname/src/qml
        patch -lp0 < $srcdir/mainpage.patch
  # new levels from Sailfish version : https://github.com/kimmoli/heebo/
  cp $srcdir/map.dat $srcdir/$_realname/
  cd $srcdir/$_realname/build/desktop

        qmake-qt4 || return 1
        make || return 1
}

package() {
    cd $srcdir

   install -d $pkgdir/usr/bin
   install -d $pkgdir/usr/share/{applications,icons,heebo}
   
   install -D -m 644 $srcdir/$_realname/doc/heebo_app_icon_256.png $pkgdir/usr/share/icons/heebo.png
   install -D -m 755 $srcdir/$_realname/build/desktop/heebo $pkgdir/usr/bin/heebo
   install -D -m 644 heebo.desktop $pkgdir/usr/share/applications/
   install -D -m 644 about.html $pkgdir/usr/share/heebo/
   install -D -m 644 help.html $pkgdir/usr/share/heebo/
}
