# Maintainer: Kivi Kaitaniemi <kivi AT ktnm DOT net>
pkgname=decman
pkgver=0.4.0
pkgrel=1
pkgdesc="Declarative package & configuration manager for Arch Linux."
arch=("any")
url="https://github.com/kiviktnm/decman"
license=("GPL3")
depends=("python" "python-requests" "devtools" "pacman" "systemd" "git")
makedepends=("python-setuptools" "python-build" "python-installer" "python-wheel")
optdepends=("less: reviewing files such as PKGBUILDs")
source=("$pkgname-$pkgver.tar.gz::https://github.com/kiviktnm/$pkgname/archive/refs/tags/$pkgver.tar.gz")
sha256sums=("64fe547dd261d9667ec074e8dc64590617a20334ee1a0f017dcd36c0058e6be3")

build() {
    cd "$pkgname-$pkgver"
    python -m build --wheel --no-isolation
}

package() {
    cd "$pkgname-$pkgver"
    python -m installer --destdir="$pkgdir" dist/*.whl
}

check() {
    cd "$pkgname-$pkgver"
    python -m unittest
}
