# Maintainer: Jimmy Tang <jtang@tchpc.tcd.ie>

pkgname=pristine-tar-git
pkgver=20130127
pkgrel=1
pkgdesc="pristine-tar can regenerate a pristine upstream tarball using only a small binary delta file and a copy of the source which can be a revision control checkout."
arch=('i686' 'x86_64')
url="http://git.kitenet.net/?p=pristine-tar.git"
license=('GPL')
makedepends=('git')
depends=('perl' 'xdelta')
provides=('pristine-tar')

_gitroot="git://git.kitenet.net/pristine-tar.git"
_gitname="pristine-tar"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  export PATH=/usr/bin/core_perl:$PATH

  perl Makefile.PL
  make
  make install DESTDIR=$pkgdir PREFIX=/usr INSTALLSITESCRIPT=/usr/bin
  install -d $pkgdir/usr/share/doc/pristine-tar
  install -D GPL TODO delta-format.txt $pkgdir/usr/share/doc/pristine-tar
}

# vim:set ts=2 sw=2 et:
