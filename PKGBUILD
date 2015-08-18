# Maintainer:  Matthew Monaco <net 0x01b dgbaley27>

_gitroot="git://github.com/dvdhrm/xorg-input-xwiimote.git"
_gitname="xorg-input-xwiimote"

pkgname=xf86-input-wiimote-git
pkgver=20120222
pkgrel=3
pkgdesc="Xorg input driver for the Nintendo Wii Remote"
url="https://github.com/dvdhrm/xorg-input-xwiimote"
license=('BSD')
groups=('xorg-drivers' 'xorg')
arch=('i686' 'x86_64')
backup=('etc/X11/xorg.conf.d/60-xorg-xwiimote.conf')
depends=('xwiimote-git' 'udev')
makedepends=('xorg-server-devel' 'git')
conflicts=("${pkgname/-git/}")
provides=("${pkgname/-git/}")
options=('!libtool')

build() {

	cd "$srcdir"

	if [[ -d "$_gitname" ]]; then
		msg2 "Cleaning and updating git repo"

		cd "$_gitname"
		git clean -dfx
		git pull

	else
		msg2 "Cloning $_gitroot"

		git clone "$_gitroot"
		cd "$_gitname"
	fi

	./autogen.sh --prefix=/usr
	make
}

package() {

	cd "$srcdir/$_gitname"

	make DESTDIR="$pkgdir" install
	install -D 60-xorg-xwiimote.conf "$pkgdir/etc/X11/xorg.conf.d/60-xorg-xwiimote.conf"
	install -D COPYING "$pkgdir/usr/share/licenses/$pkgname/COPYING"
}

# vim: set noet :
