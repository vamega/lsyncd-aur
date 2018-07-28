## Maintainer: Thermi <noel[ at ] familie-kuntze.de>
# Submitter: nullie
pkgname=lsyncd
pkgver=2.2.3
pkgrel=1
pkgdesc="Live Syncing (Mirror) Daemon"
arch=('i686' 'x86_64')
url="https://github.com/axkibe/lsyncd"
license=('GPL2')
depends=('lua52' 'rsync')
makedepends=('asciidoc' 'lua' 'cmake')
source=("https://github.com/axkibe/lsyncd/archive/release-$pkgver.tar.gz"
        'lsyncd.service'
        'FindLua.cmake.patch')

sha256sums=('7bcd0f4ae126040bb078c482ff856c87e61c22472c23fa3071798dcb1dc388dd'
            '538072a4505abbdf8c4d16c9200810d4a2253f892a71fc16b5cd7f35ebe1ae57'
            '2a60c2bfecc4be3a2e22182f6fb05748d9033454bd19c0c64cd300f74251f91c')

prepare() {
    cd $pkgname-release-$pkgver
    patch -Np1 -i "${srcdir}/FindLua.cmake.patch"
}

build() {
    cd $srcdir/$pkgname-release-$pkgver
    mkdir -p build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    make
}

package() {
    cd $srcdir/$pkgname-release-$pkgver/build
    make DESTDIR=$pkgdir install
    # fix the path of the man page. Urgh.
    install -D ${pkgdir}/usr/man/lsyncd.1 ${pkgdir}/usr/share/man/man1/lsyncd.1
    rm -rf ${pkgdir}/usr/man
    install -m 644 -D ${srcdir}/lsyncd.service ${pkgdir}/usr/lib/systemd/system/lsyncd.service
}
