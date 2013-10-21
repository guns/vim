# Maintainer: Sung Pae <self@sungpae.com>
pkgname=vim-guns
pkgver=7.4.052.75.gad927f0
pkgrel=1
pkgdesc="Sung Pae's vim build"
arch=('x86_64')
url="https://github.com/guns/vim"
license=('custom:vim')
groups=('guns')
depends=('ruby' 'python2' 'lua')
makedepends=('git' 'ruby')
conflicts=('vi' 'vim')
provides=('vim')

pkgver() {
    printf %s "$(git describe --long --tags | sed -e 's/^v//' | tr - .)"
}

build() {
    cd "$startdir"
    PREFIX=/usr PYTHON=python2 rake configure
    make -j $(grep -c ^processor /proc/cpuinfo)
}

package() {
    cd "$startdir"
    make DESTDIR="$pkgdir/" install
}
