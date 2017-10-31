# Maintainer: sekret, mail=$(echo c2VrcmV0QHBvc3Rlby5zZQo= | base64 -d)

# based on rtl8812au-dkms-git

_pkgname=rtl8812au
pkgname=$_pkgname-rpi-dkms-git
pkgver=4.3.14.r162.d57f9ef
pkgrel=1
pkgdesc="Realtek 802.11n WLAN Adapter Linux driver for rtl8812au (patched for the Raspberry Pi)"
arch=('armv7h')
url="https://github.com/ptpt52/rtl8812au"
license=('unknown')
depends=('dkms' 'linux-raspberrypi-headers')
makedepends=('git')
provides=("$_pkgname")
conflicts=("$_pkgname")
install=$pkgname.install
source=("$_pkgname::git+$url.git"
        'rpi.diff'
        'dkms.conf')
sha512sums=('SKIP'
            '15c235875ac397c4868c96118e47f2d815478b40580bdcb517e168e2682007cbe89b0513a96b978637e1947fb3143534e7356916642fbe0b692f5b76d65fb2d6'
            '4cde7f2322e49ec4291db68ee817842c46c5d412d002d2995d24df952703df0a974541535a98df09b32beb8f8ad077fc902224ea0ad9aa63e9a6c5084d6fe33e')

pkgver() {
  cd "$_pkgname"
  printf "4.3.14.r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd "$_pkgname"
  patch -i "$srcdir/rpi.diff"
}

package() {
  cd "$_pkgname"
  mkdir -p "$pkgdir/usr/src/$_pkgname-$pkgver"
  cp -a * "$pkgdir/usr/src/$_pkgname-$pkgver"

  install -Dm644 "$srcdir/dkms.conf" "$pkgdir/usr/src/$_pkgname-$pkgver"

  sed -e "s/@_PKGBASE@/$_pkgname-dkms/" -e "s/@PKGVER@/$pkgver/" -i "$pkgdir/usr/src/$_pkgname-$pkgver/dkms.conf"
}

# vim:set ts=2 sw=2 et:
