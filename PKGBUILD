# Maintainer: Emmanuel Gil Peyrot <linkmauve@linkmauve.fr>
# Contributor: Manuel Mendez <mmendez534@gmail.com>

_pkgbase=include-what-you-use
pkgname="$_pkgbase-git"
pkgver=r693.15b3f1d
pkgrel=1
pkgdesc="A tool for use with clang to analyze #includes in C and C++ source files"
url="https://include-what-you-use.org/"
license=('LLVM Release License')
arch=('i686' 'x86_64')
depends=('clang>=5.0' 'clang<5.1')
makedepends=('clang>=5.0' 'clang<5.1')
optdepends=('python: for the fix_includes.py script')
conflicts=("$_pkgbase")
provides=("$_pkgbase=0.8")

source=("$_pkgbase::git+https://github.com/include-what-you-use/include-what-you-use#branch=clang_5.0")
sha1sums=('SKIP')

pkgver() {
  cd "$srcdir/$_pkgbase"
  echo "r$(git rev-list --count HEAD).$(git rev-parse --short HEAD)"
}

prepare() {
  cd "$srcdir/$_pkgbase"
  mkdir -p build
}

build() {
  cd "$srcdir/$_pkgbase/build"
  CC=clang CXX=clang++ cmake -DIWYU_LLVM_ROOT_PATH=/usr/lib -DCMAKE_INSTALL_PREFIX=/usr ..
  make
}

package() {
  cd "$srcdir/$_pkgbase/build"

  make DESTDIR="$pkgdir" install
  install -Dm755 ../fix_includes.py "$pkgdir/usr/bin/iwyu-fix_includes.py"
}

# vim:set ts=2 sw=2 et:
