# Maintainer: Daniel M. Capella <polyzen@archlinux.org>

_name=sphinxcontrib_applehelp
pkgname=python-sphinxcontrib-applehelp
pkgver=1.0.6
pkgrel=1
pkgdesc='Sphinx extension which outputs Apple help books'
arch=('any')
url=https://github.com/sphinx-doc/sphinxcontrib-applehelp
license=('BSD')
makedepends=('python-build' 'python-flit-core' 'python-installer')
checkdepends=('python-pytest' 'python-sphinx')
source=("https://files.pythonhosted.org/packages/source/${_name::1}/$_name/$_name-$pkgver.tar.gz")
sha256sums=('a59274de7a952a99af36b8a5092352d9249279c0e3280b7dceaae8e15873c942')
b2sums=('a610774d461110704388149e0b2e1978e5d53a263df6448ee2e492ba177a5368a683823d4a512cba3dda935fc12dce7eb911fb898ac7bd053ae04b9efa4c7445')

build() {
  cd $_name-$pkgver
  python -m build --wheel --skip-dependency-check --no-isolation
}

check() {
  cd $_name-$pkgver
  pytest
}

package() {
  cd $_name-$pkgver
  python -m installer --destdir="$pkgdir" dist/*.whl

  # Symlink license file
  local site_packages=$(python -c "import site; print(site.getsitepackages()[0])")
  install -d "$pkgdir"/usr/share/licenses/$pkgname
  ln -s "$site_packages"/$_name-$pkgver.dist-info/LICENSE \
    "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
