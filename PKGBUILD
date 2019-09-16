# $Id$
# Contributor: Ionut Biru <ibiru@archlinux.org>

pkgname=vte3-ng-with-nN-cursor-move-patch
pkgver=0.58.0
pkgrel=1
pkgdesc="Virtual Terminal Emulator widget for use with GTK3"
url="https://wiki.gnome.org/Apps/Terminal/VTE"
arch=(x86_64)
license=(LGPL)
options=(!emptydirs)
depends=(gtk3 pcre2 gnutls fribidi vte-common)
makedepends=(gobject-introspection vala git gtk-doc gperf meson)
conflicts=(vte3)
provides=(vte3)
_commit=0a0abd8ff68b521fabd7dfeca3ce00a382722fcf  # tags/0.58.0
source=("git+https://gitlab.gnome.org/GNOME/vte.git/#commit=$_commit"
        "0001-expose-functions-for-pausing-unpausing-output.patch"
        "0002-expose-function-for-setting-cursor-position.patch"
        "0003-add-function-for-setting-the-text-selections.patch"
        "0004-add-functions-to-getset-block-selection-mode.patch"
        "0005-expose-function-for-getting-the-selected-text.patch"
        "0006-Add-function-to-get-selection-position.patch")
sha256sums=('SKIP'
            '51af803b893c8269a943ff520d934488073c1d28d4bf6693d386d790ec84541a'
            '604f0594c2ed9fef97483a721f8e8abf067a6a2a2fc1fd492d012e24861e0d75'
            '3f2486b08e4452421d8de58826b1cf99925514af2b95abaf1b34d081bc3eb1d8'
            'e74d000a729eabf31f4aabd08433790a7700fcccb6f302916992fb750f3d28ea'
            'a6d90ac8d391d6906dbed22041c597176366501ff625a1b222f1fcf9f83e78f4'
            'e02da4f83aab8b4fcdab5adb2099de246c4d8c3864381e5847e11117c5848246')

pkgver() {
  cd vte
  git describe --tags | sed 's/-/+/g'
}

prepare() {
  cd vte

  patch -p1 -i ${srcdir}/0001-expose-functions-for-pausing-unpausing-output.patch
  patch -p1 -i ${srcdir}/0002-expose-function-for-setting-cursor-position.patch
  patch -p1 -i ${srcdir}/0003-add-function-for-setting-the-text-selections.patch
  patch -p1 -i ${srcdir}/0004-add-functions-to-getset-block-selection-mode.patch
  patch -p1 -i ${srcdir}/0005-expose-function-for-getting-the-selected-text.patch
  patch -p1 -i ${srcdir}/0006-Add-function-to-get-selection-position.patch
}

build() {
  arch-meson vte build -D docs=true
  ninja -C build
}

package() {
  DESTDIR="$pkgdir" meson install -C build

  rm "$pkgdir"/etc/profile.d/vte.sh
}
