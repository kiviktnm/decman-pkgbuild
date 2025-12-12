# Maintainer: Kivi Kaitaniemi <kivi AT ktnm DOT net>
pkgname=decman
pkgver=0.4.1
pkgrel=1
pkgdesc="Declarative package & configuration manager for Arch Linux."
arch=("any")
url="https://github.com/kiviktnm/decman"
license=("GPL3")
depends=("python" "python-requests" "devtools" "pacman" "systemd" "git")
makedepends=("python-setuptools" "python-build" "python-installer" "python-wheel")
optdepends=("less: reviewing files such as PKGBUILDs")
source=("$pkgname-$pkgver.tar.gz::https://github.com/kiviktnm/$pkgname/archive/refs/tags/$pkgver.tar.gz")
sha256sums=("3fa76459f11a676c44a184a10c7deb4a26ceebcceefca19854c45ffecc4d4133")

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
