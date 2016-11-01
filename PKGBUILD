pkgname=streamlink-git
_pkgname=streamlink
pkgver=0.0.2.r11.g5f9045a
pkgrel=1
pkgdesc='CLI program that launches streams from various streaming services in a custom video player'
arch=('any')
url='https://github.com/streamlink/streamlink'
license=('BSD')
depends=('python-requests' 'rtmpdump' 'python-setuptools')
makedepends=('python-sphinx')
optdepends=('python-librtmp: Required by the ustreamtv plugin to be able to use non-mobile streams.')
conflicts=('streamlink')
source=(git+https://github.com/streamlink/streamlink
        goodgame.py)
sha256sums=('SKIP'
            '272f4ebc6c11ceade081f8bdd2062a79b888d0e967264272c2d4c36f77fa1916')
prepare() {
  cp goodgame.py "${srcdir}/${_pkgname}/src/streamlink/plugins/"
}
pkgver() {
  cd "${srcdir}/${_pkgname}"
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}
build() {
  cd "${srcdir}/${_pkgname}"
  python setup.py build_sphinx -b man
}
package() {
  cd "${srcdir}/${_pkgname}"
  python setup.py install --root="$pkgdir" --optimize=1
  install -Dm644 build/sphinx/man/streamlink.1 \
    "$pkgdir/usr/share/man/man1/streamlink.1"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
