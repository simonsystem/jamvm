# Maintainer: Simon Schroeter <simon.schroeter@gmail.com>
# Contributor: Samuel Tardieu <sam@rfc1149.net>
# Contributor: ArLi Weng <arliweng@gmail.com>
# Contributor: Sean Gillespie <Sean.D.Gillespie@gmail.com>
# Contributor: Roberto Alsina <ralsina@kde.org>

pkgname=jamvm
pkgver=2.0.0
pkgrel=1
pkgdesc="A Compact Java Virtual Machine which conforms to the JVM 
specification"
arch=('i686' 'x86_64')
url="http://jamvm.sourceforge.net/"
license=("GPL")
depends=('classpath' 'zlib' 'libffi')
makedepends=('pkg-config')
source=("http://downloads.sourceforge.net/sourceforge/jamvm/$pkgname-$pkgver.tar.gz")
md5sums=('a6e3321ef4b3cfb4afc20bd75452e11e')

build() {
    cd $srcdir/$pkgname-$pkgver
    export CFLAGS="$CFLAGS `pkg-config libffi --cflags`"
    ./configure --with-classpath-install-dir=/usr --prefix=/usr --enable-ffi
    make
}
package() {
    cd $srcdir/$pkgname-$pkgver
    make DESTDIR=$pkgdir install
    # Avoid conflict with classpath (which jamvm requires)
    install -D $pkgdir/usr/include/jni.h $pkgdir/usr/include/jamvm/jni.h
    rm $pkgdir/usr/include/jni.h
}
