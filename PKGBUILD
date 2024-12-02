# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>

_offline="false"
_git="false"
_py="python"
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
_pkg=evm-contracts-abi-get
pkgname="${_pkg}-git"
pkgver=0.0.0.0.0.0.0.0.0.0.0.1.1.1.1
_aioetherscan_ver="0.9.5.3"
_commit="e8654948a72b6d1db66a887ad9c9f7c1bb2ab9b3"
pkgrel=1
_pkgdesc=(
  "Returns ABI of a smart contract on an EVM network."
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  any
)
_http="https://github.com"
_ns="themartiancompany"
url="${_http}/${_ns}/${pkgname}"
license=(
  AGPL3
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
  "${_py}-aioetherscan>=${_aioetherscan_ver}"
)
_os="$( \
  uname \
    -o)"
[[ "${_os}" != "GNU/Linux" ]] && \
[[ "${_os}" == "Android" ]] && \
  depends+=(
  )
optdepends=(
)
[[ "${_os}" == 'Android' ]] && \
  optdepends+=(
  )
makedepends=(
  "${_py}-setuptools"
)
checkdepends=(
  "shellcheck"
)
provides=(
  "${_pkg}=${pkgver}"
  "${_py}-${_pkg}=${pkgver}"
)
conflicts=(
  "${_pkg}"
  "${_py}-${_pkg}"
)
_url="${url}"
_tag="master"
_tag_name="branch"
_tarname="${pkgname}-${_tag}"
[[ "${_offline}" == "true" ]] && \
  _url="file://${HOME}/${_pkg}"
if [[ "${_git}" == true ]]; then
  makedepends+=(
    "git"
  )
  _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
  _sum="SKIP"
elif [[ "${_git}" == false ]]; then
  if [[ "${_tag_name}" == 'pkgver' ]]; then
    _src="${_tarname}.tar.gz::${_url}/archive/refs/tags/${_tag}.tar.gz"
    _sum="d4f4179c6e4ce1702c5fe6af132669e8ec4d0378428f69518f2926b969663a91"
  elif [[ "${_tag_name}" == "commit" ]]; then
    _src="${_tarname}.zip::${_url}/archive/${_commit}.zip"
    _sum='31ac0b8014076f8c7cafa1c92c311359dc7f6f931e17c0a718c406cae77272f7'
  fi
fi
source=(
  "${_src}"
)
sha256sums=(
  "${_sum}"
)
validpgpkeys=(
  # Truocolo <truocolo@aol.com>
  '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
  # Pellegrino Prevete <pellegrinoprevete@gmail.com>
  'E30813C918EDD358EFCDCA34D3104DE92EB34492'
)

check() {
  cd \
    "${_tarname}"
  make \
    -k \
    check
}

# shellcheck disable=SC2154
package() {
  cd \
    "${_tarname}"
  "${_py}" \
    setup.py \
    install \
    --root="${pkgdir}" \
    --optimize=1
}

# vim: ft=sh syn=sh et
