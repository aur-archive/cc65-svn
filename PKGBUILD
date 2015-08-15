pkgname=cc65-svn
pkgver=5657
pkgrel=1
pkgdesc="C compiler for 6502 family microprocessors"
depends=()
arch=('i686' 'x86_64')
license=('custom')
url="http://www.cc65.org/"
makedepends=("subversion" "linuxdoc-tools")
source=(patch.diff license)


_svntrunk="svn://svn.cc65.org/cc65/trunk"
_svnmod="cc65"

build() {
	msg "Connecting to SVN server..."
	if [ -d ${_svnmod}/.svn ]; then
		(cd "${_svnmod}" && svn cleanup && svn update)
	else
		svn co ${_svntrunk} ${_svnmod}
	fi

	cd $srcdir/cc65 || return 1
	patch -p1 < ../../patch.diff || return 1
    
	make -f make/gcc.mak || return 1
    
}

package() {
	cd $srcdir/cc65 || return 1

	make -f make/gcc.mak DEST_DIR=$pkgdir install || return 1

	mkdir -p $pkgdir/usr/share/licenses/$pkgname/
	cp $srcdir/license $pkgdir/usr/share/licenses/$pkgname/
}

md5sums=('0ade7f1fbf8d809d5dbaa64cb5c9dede' '8319a72050fb79daf7e1b2bcf5a9e69d')

