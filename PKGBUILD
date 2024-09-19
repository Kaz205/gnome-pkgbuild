pkgbase=mutter
pkgname=(
  mutter
)
pkgver=47.0
pkgrel=1
pkgdesc="Window manager and compositor for GNOME"
url="https://gitlab.gnome.org/GNOME/mutter"
arch=(x86_64)
license=(GPL-2.0-or-later)
depends=(
  at-spi2-core
  cairo
  colord
  dconf
  fontconfig
  fribidi
  gcc-libs
  gdk-pixbuf2
  glib2
  glibc
  gnome-desktop-4
  gnome-settings-daemon
  graphene
  gsettings-desktop-schemas
  gtk4
  harfbuzz
  iio-sensor-proxy
  lcms2
  libcanberra
  libcolord
  libdisplay-info
  libdrm
  libei
  libglvnd
  libgudev
  libice
  libinput
  libpipewire
  libsm
  libsysprof-capture
  libwacom
  libx11
  libxau
  libxcb
  libxcomposite
  libxcursor
  libxdamage
  libxext
  libxfixes
  libxi
  libxinerama
  libxkbcommon
  libxkbcommon-x11
  libxkbfile
  libxrandr
  libxtst
  mesa
  pango
  pipewire
  pixman
  python
  startup-notification
  systemd-libs
  wayland
  xorg-xwayland
)
makedepends=(
  egl-wayland
  gi-docgen
  git
  glib2-devel
  gobject-introspection
  meson
  sysprof
  wayland-protocols
)
source=("git+https://github.com/Kaz205/mutter.git#branch=gnome-47"
	"git+https://gitlab.gnome.org/GNOME/gvdb.git#commit=b54bc5da25127ef416858a3ad92e57159ff565b3")
b2sums=('SKIP' 'SKIP')
options=('lto')

prepare() {
  cd mutter
}

build() {
  local meson_options=(
    -D egl_device=true
    -D installed_tests=false
    -D libdisplay_info=enabled
    -D tests=disabled
    -D wayland_eglstream=true
    -D profiler=false
#    -D verbose=false
  )

  CFLAGS="${CFLAGS/-O2/-O3} -fno-semantic-interposition"
  LDFLAGS+=" -Wl,-Bsymbolic-functions"

  # Inject gvdb
  export MESON_PACKAGE_CACHE_DIR="$srcdir"

  arch-meson mutter build "${meson_options[@]}"
  meson compile -C build
}

package_mutter() {
  provides=(libmutter-15.so)

  meson install -C build --destdir "$pkgdir"
}
