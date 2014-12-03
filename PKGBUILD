# Maintainer: Sung Pae <self@sungpae.com>
pkgname=('vim-guns' 'vim-nox-guns')
pkgver=
pkgrel=1
pkgdesc="Sung Pae's vim build"
arch=('x86_64')
url="https://github.com/guns/vim"
license=('custom:vim')
groups=('guns')
makedepends=('git' 'ruby')
conflicts=('vim')
provides=('vim')

pkgver() {
    printf %s "$(git describe --long --tags | sed -e 's/^v//' | tr - .)"
}

__build__() {
    cd "$startdir"
    make DESTDIR="$pkgdir/" -j $(grep -c ^processor /proc/cpuinfo) install
}

package_vim-guns() {
    depends=('ncurses' 'ruby' 'python2' 'lua' 'gpm' 'libx11' 'libsm' 'libice' 'libxt')
    PREFIX=/usr PYTHON=python2 rake configure
    __build__
}

package_vim-nox-guns() {
    depends=('ncurses' 'ruby' 'python2' 'lua' 'gpm')
    PREFIX=/usr PYTHON=python2 NOX=1 rake configure
    __build__
}
