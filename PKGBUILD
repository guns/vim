# Maintainer: Sung Pae <self@sungpae.com>
pkgname=vim
pkgver=v7.4.052.74.gb85d2e1.guns
pkgrel=1
pkgdesc="Sung Pae's vim build"
arch=('x86_64')
url="https://github.com/guns/vim"
license=('custom:vim')
depends=('ruby' 'python2' 'lua')
makedepends=('git')
conflicts=('vi')

pkgver() {
    printf '%s.guns' "$(git describe --long --tags | tr - .)"
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
