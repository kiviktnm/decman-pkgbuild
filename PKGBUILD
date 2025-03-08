# Maintainer: Kivi Kaitaniemi <kivi AT ktnm DOT net>
pkgname=decman
pkgver=0.3.3
pkgrel=1
pkgdesc="Declarative package & configuration manager for Arch Linux."
arch=("any")
url="https://github.com/kiviktnm/decman"
license=("GPL3")
depends=("python" "python-requests" "devtools" "pacman" "systemd" "git")
makedepends=("python-setuptools" "python-build" "python-installer" "python-wheel")
optdepends=("less: reviewing files such as PKGBUILDs")
source=("$pkgname-$pkgver.tar.gz::https://github.com/kiviktnm/$pkgname/archive/refs/tags/$pkgver.tar.gz")
sha256sums=("e415040f3a32fb5c4286ed28bbf71a75a39a79f7a5426447318d17351c5634c6")

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
