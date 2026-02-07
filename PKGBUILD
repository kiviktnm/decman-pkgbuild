# Maintainer: Kivi Kaitaniemi <kivi AT ktnm DOT net>
pkgname=decman
pkgver=1.1.0
pkgrel=1
pkgdesc="Declarative package & configuration manager for Arch Linux."
arch=("any")
url="https://github.com/kiviktnm/decman"
license=("GPL3")
depends=("python" "python-requests" "pyalpm" "devtools" "pacman" "systemd" "git" "less")
makedepends=("python-setuptools" "python-build" "python-installer" "python-wheel")
checkdepends=("python-pytest" "python-pytest-mock")
optdepends=("flatpak: manage flatpak packages")
source=("$pkgname-$pkgver.tar.gz::https://github.com/kiviktnm/$pkgname/archive/refs/tags/$pkgver.tar.gz")
sha256sums=("21cf226a4e865b8ce547d06d13cc277ca509b36cfea32550b9577df4f2a134c0")

build() {
    cd "$pkgname-$pkgver"
    python -m build --wheel --no-isolation

    # plugins
    python -m build --wheel --no-isolation plugins/decman-pacman
    python -m build --wheel --no-isolation plugins/decman-systemd
    python -m build --wheel --no-isolation plugins/decman-flatpak
}

package() {
    cd "$pkgname-$pkgver"
    python -m installer --destdir="$pkgdir" dist/*.whl

    # plugins
    python -m installer --destdir="$pkgdir" plugins/decman-pacman/dist/*.whl
    python -m installer --destdir="$pkgdir" plugins/decman-systemd/dist/*.whl
    python -m installer --destdir="$pkgdir" plugins/decman-flatpak/dist/*.whl

    install -Dm644 completions/decman.bash "$pkgdir/usr/share/bash-completion/completions/decman"
    install -Dm644 completions/_decman "$pkgdir/usr/share/zsh/site-functions/_decman"
    install -Dm644 completions/decman.fish "$pkgdir/usr/share/fish/vendor_completions.d/decman.fish"
}

check() {
    cd "$pkgname-$pkgver"

    # run tests in a virtual env
    python -m venv --system-site-packages test-env

    test-env/bin/python -m installer dist/*.whl
    test-env/bin/python -m installer plugins/decman-pacman/dist/*.whl
    test-env/bin/python -m installer plugins/decman-systemd/dist/*.whl
    test-env/bin/python -m installer plugins/decman-flatpak/dist/*.whl

    # flatpak has no tests
    test-env/bin/python -P -m pytest tests
    test-env/bin/python -P -m pytest plugins/decman-pacman/tests
    test-env/bin/python -P -m pytest plugins/decman-systemd/tests
}
