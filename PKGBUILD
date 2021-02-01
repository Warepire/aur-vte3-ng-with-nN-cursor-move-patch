# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Contributor: Ionut Biru <ibiru@archlinux.org>

pkgname=vte3-ng-with-nN-cursor-move-patch
pkgver=0.62.2
pkgrel=1
pkgdesc="Virtual Terminal Emulator widget"
url="https://wiki.gnome.org/Apps/Terminal/VTE"
arch=(x86_64)
license=(LGPL)
depends=(gtk3 pcre2 gnutls fribidi systemd-libs vte-common)
makedepends=(gobject-introspection vala git gtk-doc gperf meson)
conflicts=(vte3)
provides=(vte3 libvte-2.91.so)
_commit=73713ec0644e232fb740170e399282be778d97f9  # tags/0.62.2
source=("git+https://gitlab.gnome.org/GNOME/vte.git/#commit=$_commit"
        "0001-expose-functions-for-pausing-unpausing-output.patch"
        "0002-expose-function-for-setting-cursor-position.patch"
        "0003-add-function-for-setting-the-text-selections.patch"
        "0004-add-functions-to-getset-block-selection-mode.patch"
        "0005-expose-function-for-getting-the-selected-text.patch"
        "0006-Add-function-to-get-selection-position.patch")
sha256sums=('SKIP'
            '4dd0ed5124e0877df25f5d61922ad0f2e7d1bdbceed253791a5a337b92a4a892'
            'cbd53d0ce4bb1995bfa74af68bc2569258335dc8d79e74159973a4a33a084d2f'
            '3bf1ba12795fa482b4b477b57ea43015c4a887480e79eb11251d7c3f661dc69e'
            '43600aa2fe4ad522ce0a072d229b15f8f4e3160db82f167cdae81e640e9c571e'
            'fd399292564c1d71a124d46e3207b2dafa0038bb6bc63bb1f1ccf02258d57856'
            '5b79912abf7b8454e328ac438a9013bf849e10a51d99534d3d6eb5d3cf59848a')

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
  arch-meson vte build -D docs=true -D b_lto=false
  ninja -C build
}

package() {
  DESTDIR="$pkgdir" meson install -C build

  rm -r "$pkgdir"/etc/profile.d
  rm -r "$pkgdir"/usr/lib/{systemd,vte-urlencode-cwd}
}
