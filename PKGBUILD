# Maintainer: Sung Pae <self@sungpae.com>
pkgname=('vim-nerv' 'vim-nox-nerv')
pkgver=0
pkgrel=1
pkgdesc="Custom vim build"
arch=('x86_64')
url="https://github.com/guns/vim"
license=('custom:vim')
groups=('nerv')
makedepends=('git' 'ruby')
conflicts=('vim')
provides=('vim')
replaces=('vim-guns')

pkgver() {
    printf %s "$(git describe --long --tags | sed -e 's/^v//' | tr - .)"
}

__build__() {
    cd "$startdir"
    make DESTDIR="$pkgdir/" -j $(grep -c ^processor /proc/cpuinfo) install
}

package_vim-nerv() {
    depends=('ncurses' 'ruby' 'python2' 'lua' 'gpm' 'libx11' 'libsm' 'libice' 'libxt')
    PREFIX=/usr PYTHON=python2 rake configure
    __build__
}

package_vim-nox-nerv() {
    depends=('ncurses' 'ruby' 'python2' 'lua' 'gpm')
    PREFIX=/usr PYTHON=python2 NOX=1 rake configure
    __build__
}
