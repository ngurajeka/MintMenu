# Maintainer: twa022 <twa022 at gmail dot com>
# Contributor: Giuseppe Borzi <gborzi _AT_ ieee _DOT_ org>
# Contributor: ryooichi <ryooichi+arch AT gmail DOT com>
# Real thanks goes to jelly, mike_93 and the original creators of mintmenu, usp, slab...
# See also:
#   http://bbs.archlinux.org/viewtopic.php?id=66987
#   http://bbs.archlinux.org/viewtopic.php?id=68633
#   http://github.com/jelly/archmenu

pkgname=mintmenu
pkgver=5.4.1
pkgrel=1
pkgdesc="Linux Mint Menu for MATE"
arch=('i686' 'x86_64')
url="http://packages.linuxmint.com/pool/main/m/mintmenu"
license=('GPL')
depends=('mate-panel>=1.6.0' 'python2-gobject' 'archlinux-artwork' 'gksu' 'python2-xdg' 'xdg-utils' 'python2-keybinder2')
optdepends=('mate-menu-editor: for editing the gnome menu'
            'mint-translations: translations files'
            'gnome-packagekit: package manager button'
            'mate-screensaver: lock screen button')
source=("${url}/${pkgname}_${pkgver}.tar.gz" 
        'arch-patch.diff'
        'execute_fix.diff'
        'removescript')
install=${pkgname}.install

package() {
  cd "$srcdir/${pkgname}"
  #patch -uNp2 -r- -i "$srcdir/arch-patch.diff"
  patch -uNp2 -r- -i "$srcdir/execute_fix.diff"
  rm -f usr/lib/linuxmint/mintMenu/*.pyc usr/lib/linuxmint/mintMenu/plugins/*pyc
  #sed -i -e "s/__version__/$pkgver/" usr/lib/linuxmint/mintMenu/mintMenu.py
  cp -R usr "$pkgdir/"
  install -m755 "$srcdir/removescript" "$pkgdir/usr/lib/linuxmint/mintMenu/"
  for i in $(find . -name '*.py') ; do
    sed -ri 's:^#!/usr/bin/(env )?python$:&2:' "$i"
  done
  cd "$pkgdir"/usr/lib/linuxmint/mintMenu
  ./compile.py
}

sha256sums=('SKIP'
            '57b322e658742f797630ac6d0d0997f5a6e99b54dbaa80c121521701d81cc265'
            '2115ec0202745e415daefadc9d3096f32b20ab3d6b782342880a6e3877fdf0e8'
            '9533d0f5416af1f2b8ef5097f06e39135278eef856994d859c4ee7ba57d6fcaa')
