# Maintainer: Stefano Facchini <stefano.facchini@gmail.com>
pkgname=office-runner-git
pkgver=20130128
pkgrel=1
pkgdesc="Office game for laptop owners"
arch=('i686' 'x86_64')
url="http://www.gnome.org"
license=('GPL3')
depends=('gtk3' 'gnome-settings-daemon')
makedepends=('git')
provides=('office-runner')
conflicts=('office-runner')

_gitroot=git://git.gnome.org/office-runner
_gitname=office-runner

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  ./autogen.sh --prefix=/usr
  make
}

package() {
  cd "$srcdir/$_gitname-build"
  make DESTDIR="$pkgdir/" install
}

# vim:set ts=2 sw=2 et:
