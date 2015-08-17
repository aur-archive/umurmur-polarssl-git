# Maintainer: kleim <kleim8 at yahoo dot fr>

pkgname=umurmur-polarssl-git
_gitname=umurmur
pkgver=0.2.14.r36.g75f01c6
pkgrel=1
pkgdesc="A minimalistic Mumble server (PolarSSL version)"
arch=('i686' 'x86_64')
url="https://github.com/fatbob313/umurmur"
license=('GPL')
depends=('libconfig' 'protobuf-c' 'polarssl')
makedepends=('git')
conflicts=('umurmur')
provides=('umurmur')
source=(git://github.com/fatbob313/umurmur.git
        umurmur.service
        umurmur.1)
md5sums=('SKIP'
         '5dabe54621dc5bc74f48f08dc045c395'
         'fa4ce7a44e03641b638d5b098942e969')

pkgver() {
  cd $_gitname
  git describe --long | sed -r 's/([^-]*-g)/r\1/;s/-/./g'
}

build() {
    cd $_gitname
    ./autogen.sh
    ./configure --prefix=/usr --mandir=/usr/share/man --with-ssl=polarssl
    make
}

package() {
    cd $_gitname
    make PREFIX=/usr DESTDIR=${pkgdir} install
     
    install -Dm644 umurmur.conf.example ${pkgdir}/etc/umurmur/umurmur.conf.example
    install -Dm755 ${srcdir}/umurmur.service ${pkgdir}/usr/lib/systemd/system/umurmur.service
    install -Dm644 ${srcdir}/umurmur.1 ${pkgdir}/usr/share/man/man1/umurmur.1
} 

