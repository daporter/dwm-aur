# Maintainer: Neptune <neptune650@proton.me>
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Dag Odenhall <dag.odenhall@gmail.com>
# Contributor: Grigorios Bouzakis <grbzks@gmail.com>

pkgname=dwm
pkgver=6.4
pkgrel=2
pkgdesc="A dynamic window manager for X"
url="https://dwm.suckless.org"
arch=('i686' 'x86_64' 'arm' 'armv7h' 'armv6h' 'aarch64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2')
install=dwm.install
source=(dwm.desktop
        https://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
        config.h
        https://dwm.suckless.org/patches/shift-tools/shift-tools.c
        https://dwm.suckless.org/patches/titlecolor/dwm-titlecolor-20210815-ed3ab6b4.diff
        https://dwm.suckless.org/patches/uselessgap/dwm-uselessgap-20211119-58414bee958f2.diff)
sha256sums=('bc36426772e1471d6dd8c8aed91f288e16949e3463a9933fee6390ee0ccd3f81'
            'fa9c0d69a584485076cfc18809fd705e5c2080dafb13d5e729a3646ca7703a6e'
            '735e0191e9edda363c32edecb3f4e85460427397cb0a828e18b024e852ac6b5c'
            'ea03163c888c15fb3e7fe847ac8bb3fd13bbb4fe7982157b9227bdf11ae10306'
            '08974ad6fb8f32938b7a793ecc6e281c7bbdfe8f40d1ed52c2ef31f62738f5c6'
            '80cb7a75ae1f38fe7ca167d636fb8e90506dddd6165c2f32cbb0dd1b02eff576')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"
  if [[ -f "$srcdir/config.h" ]]; then
    cp -fv "$srcdir/config.h" config.h
  fi
  if [[ -f "$srcdir/shift-tools.c" ]]; then
    cp -fv "$srcdir/shift-tools.c" shift-tools.c
  fi
  patch --forward --strip=1 --input="${srcdir}/dwm-titlecolor-20210815-ed3ab6b4.diff"
  patch --forward --strip=1 --input="${srcdir}/dwm-uselessgap-20211119-58414bee958f2.diff"
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
  install -Dm644 "$srcdir/dwm.desktop" "$pkgdir/usr/share/xsessions/dwm.desktop"
}
