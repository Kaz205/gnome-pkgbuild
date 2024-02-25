# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Contributor: Ionut Biru <ibiru@archlinux.org>
# Contributor: Michael Kanis <mkanis_at_gmx_dot_de>

pkgbase=mutter
pkgname=(
  mutter
)
pkgver=45.4
pkgrel=1
pkgdesc="Window manager and compositor for GNOME"
url="https://gitlab.gnome.org/GNOME/mutter"
arch=(x86_64)
license=(GPL-2.0-or-later)
depends=(
  colord
  dconf
  gnome-desktop-4
  gnome-settings-daemon
  graphene
  gsettings-desktop-schemas
  iio-sensor-proxy
  lcms2
  libcanberra
  libdisplay-info
  libei
  libgudev
  libinput
  libsm
  libsysprof-capture
  libxkbcommon-x11
  libxkbfile
  pipewire
  startup-notification
  xorg-xwayland
)
makedepends=(
  egl-wayland
  git
  gobject-introspection
  gtk3
  meson
  sysprof
  wayland-protocols
  xorg-server
  xorg-server-xvfb
)
checkdepends=(
  gnome-session
  python-dbusmock
  wireplumber
  zenity
)
source=("git+https://github.com/Kaz205/mutter.git#branch=gnome-45")
b2sums=('SKIP')

prepare() {
  cd mutter
}

build() {
  local meson_options=(
    -D egl_device=true
    -D installed_tests=false
    -D libdisplay_info=true
    -D wayland_eglstream=true
    -D profiler=false
    -D tests=false
#    -D verbose=false
  )

  CFLAGS="${CFLAGS/-O2/-O3} -fno-semantic-interposition"
  LDFLAGS+=" -Wl,-Bsymbolic-functions"

  arch-meson mutter build "${meson_options[@]}"
  meson compile -C build
}

package_mutter() {
  provides=(libmutter-13.so)

  meson install -C build --destdir "$pkgdir"
}
