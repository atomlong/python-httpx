# Maintainer: Eli Schwartz <eschwartz@archlinux.org>

_pkgname=httpx
pkgname=python-httpx
pkgver=0.21.1
pkgrel=1
pkgdesc="A next generation HTTP client for Python"
arch=('any')
url="https://github.com/encode/${_pkgname}"
license=('BSD')
depends=('python-charset-normalizer' 'python-httpcore' 'python-idna' 'python-rfc3986' 'python-sniffio')
optdepends=('python-brotlicffi: for brotli response decompression')
makedepends=('python-setuptools')
checkdepends=('python-pytest-asyncio' 'python-pytest-trio' 'python-typing_extensions' 'python-brotlicffi' 'python-h2' 'python-trustme' 'uvicorn')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/${pkgver}.tar.gz"
        "0001-Do-not-override-the-system-SSL-certificates-with-the.patch")
sha512sums=('a4f737f6c6ae909fd3ea811e0ff3b78ed6496da8d797ef49746f744216e055f8225d613fe935d5e2780aa1b233053ad436e8849eef578e662ca8ee34513ad12e'
            'faf90f908ab8d5054d096eef1ba4e9cee733eb8178d2df0dfe922923bf8a98eebf880b9a6be3386caffed88229f82f1199c026ede455a57998246821a37e5748')
b2sums=('c3c800657abaed461ab6f44e3cd9799be4b6499070a5db2ee8d5d61c776d86591c74192eb1c88d4072dc361ea4c9448a3ed061c715fa4504fc931fdd96ccde62'
        '3e020b5f3c3aeeede6304851023eed4ab10f74df68203b504b5564892aa960d5c52521279a0b9cf40ead1e18b5ce9ee3998ad4502e6008f07808817d0405b7c7')

prepare() {
    cd "${srcdir}"/${_pkgname}-${pkgver}

    # bad certifi
    patch -p1 -i ../0001-Do-not-override-the-system-SSL-certificates-with-the.patch
}

build() {
    cd "${srcdir}"/${_pkgname}-${pkgver}

    python setup.py build
}

check() {
    cd "${srcdir}"/${_pkgname}-${pkgver}

    python -m pytest
}

package() {
    cd "${srcdir}"/${_pkgname}-${pkgver}

    python setup.py install --root="${pkgdir}" --optimize=1 --skip-build
    install -Dm644 LICENSE.md "${pkgdir}"/usr/share/licenses/${pkgname}/LICENSE.md
}
