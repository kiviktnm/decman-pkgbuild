# Maintainer: Kivi Kaitaniemi <kivi AT ktnm DOT net>
pkgname=decman-git
pkgver=0.1.2
pkgrel=1
pkgdesc="Declarative package & configuration manager for Arch Linux."
arch=("any")
url="https://github.com/kiviktnm/decman"
license=("GPL3")
depends=("python" "python-requests" "devtools" "pacman" "systemd" "git")
makedepends=("python-setuptools" "python-build" "python-installer" "python-wheel")
optdepends=("less: reviewing files such as PKGBUILDs")
source=("$pkgname::git+https://github.com/kiviktnm/decman.git")
sha256sums=("SKIP")
provides=("decman")
conflicts=("decman")

pkgver() {
    cd "$pkgname"
    git describe --long --tags --abbrev=7 | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
    cd "$pkgname"
    python -m build --wheel --no-isolation
}

package() {
    cd "$pkgname"
    python -m installer --destdir="$pkgdir" dist/*.whl
}

check() {
    cd "$pkgname"
    python -m unittest
}
