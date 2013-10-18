# Maintainer: Sung Pae <self@sungpae.com>
pkgname=vim
pkgver=7.4.052.74.g8478fa4.guns
pkgrel=1
pkgdesc="Sung Pae's vim build"
arch=('x86_64')
url="https://github.com/guns/vim"
license=('custom:vim')
groups=('guns')
depends=('ruby' 'python2' 'lua')
makedepends=('git')
conflicts=('vi')

pkgver() {
    printf '%s.guns' "$(git describe --long --tags | sed -e 's/^v//' | tr - .)"
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
