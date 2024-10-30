# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=sphinxcontrib-applehelp
_Pkg="sphinxcontrib_applehelp"
pkgname="${_py}-${_pkg}"
pkgver=2.0.0
pkgrel=1
pkgdesc='Sphinx extension which outputs Apple help books'
arch=(
  any
)
_http="https://github.com"
_ns="sphinx-doc"
url="${_http}/${_ns}/${_pkg}"
license=(
  BSD-2-Clause
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  git
  "${_py}-build"
  "${_py}-flit-core"
  "${_py}-installer"
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-sphinx"
)
source=(
  "${_pkg}-${pkgver}::git+${url}.git#tag=$pkgver"
)
b2sums=(
  '152bb60660b0b3ed301e818c617c05fa23c3fae888aeae4eeb3ba1cad0fddeafda1658c55c10ddbad5530f5fc9c6cb0a6349b8e4ac484899876af7b926eb8f95'
)

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --skip-dependency-check \
    --no-isolation
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  pytest
}

package() {
  local \
    _site_packages
  _site_packages=$( \
    "${_py}" \
      -c \
        "import site; print(site.getsitepackages()[0])")
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  # Symlink license file
  install \
    -dm755 \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  ln \
    -s \
    "${_site_packages}/${_Pkg}-${pkgver}.dist-info/LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
