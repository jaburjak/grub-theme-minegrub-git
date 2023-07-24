# Maintainer: Jakub Jabůrek <jaburek.jakub@gmail.com>

pkgname=grub-theme-minegrub-git
pkgver=1.2.0
pkgrel=1
pkgdesc='A Grub Theme in the style of Minecraft!'
arch=('any')
url='https://github.com/Lxtharia/minegrub-theme'
license=('MIT')
depends=('grub' 'neofetch' 'python' 'python-pillow')
makedepends=('git')
provides=('grub-theme-minegrub')
conflicts=('grub-theme-minegrub')
source=("${pkgname}::git+${url}.git")
sha256sums=('SKIP')
_themedir='/usr/share/grub/themes/minegrub/'

prepare() {
	cd "$pkgname"
	git checkout $(git tag --sort=taggerdate | grep -E '[0-9]' | tail -1)

	sed -i "s%/boot/grub/themes/minegrub-theme/%$_themedir%g" assets/minegrub-update.service
}

pkgver() {
	cd "$pkgname"
	git describe --tags | cut -b 2-7
}

package() {
	cd "$pkgname"

	mkdir -p "$pkgdir/$_themedir"
	cp -r * "$pkgdir/$_themedir"

	install -Dt "$pkgdir/etc/systemd/system/" assets/minegrub-update.service

	install -Dt "$pkgdir/usr/share/licenses/$pkgname/" LICENSE
}
