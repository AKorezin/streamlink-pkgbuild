pkgname=livestreamer-git
_pkgname=livestreamer
pkgver=r1474.ab80dbd
pkgrel=1
pkgdesc='CLI program that launches streams from various streaming services in a custom video player'
arch=('any')
url='https://github.com/chrippa/livestreamer'
license=('BSD')
depends=('python-requests' 'rtmpdump' 'python-setuptools')
makedepends=('python-sphinx')
conflicts=('livestreamer')
source=(git+https://github.com/chrippa/livestreamer)
sha256sums=('SKIP')
prepare() {
	cd "${srcdir}/${_pkgname}"
	git fetch origin pull/1461/head:1461
	git merge 1461
}
pkgver() {
	cd "${srcdir}/${_pkgname}"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}
build() {
	cd "${srcdir}/${_pkgname}"
	python setup.py build_sphinx -b man
}
package() {
	cd "${srcdir}/${_pkgname}"
	python setup.py install --root="$pkgdir" --optimize=1

	install -Dm644 build/sphinx/man/livestreamer.1 \
	"$pkgdir/usr/share/man/man1/livestreamer.1"

	install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
