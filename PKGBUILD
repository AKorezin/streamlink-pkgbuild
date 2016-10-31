pkgname=streamlink-git
_pkgname=streamlink
pkgver=r1590.5f9045a
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
            'SKIP')
prepare() {
  cp goodgame.py "${srcdir}/${_pkgname}/src/streamlink/plugins/"
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
  install -Dm644 build/sphinx/man/streamlink.1 \
    "$pkgdir/usr/share/man/man1/streamlink.1"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
