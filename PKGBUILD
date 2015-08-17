# Maintainer: gee
pkgname=sgminer-dev-git
pkgver=5.0.0.r6.ge481d67
pkgrel=2
pkgdesc="A multi-threaded multi-pool GPU miner for various algorithms-based coins."
arch=('i686' 'x86_64')
url="https://github.com/sgminer-dev/"
license=('GPL3')
source=("git+https://github.com/sgminer-dev/sgminer.git")
depends=('curl' 'libcl' 'libtool' 'pkg-config')
makedepends=('opencl-headers')
optdepends=('ncurses: For ncurses formatted screen output'
            'sgminer-adl-sdl: AMD ADL needed for GPU control with Catalyst'
            'opencl-nvidia: OpenCL implementation for NVIDIA'
            'opencl-catalyst: OpenCL implementation for AMD')
provides=('sph-sgminer' 'sgminer')
sha512sums=('SKIP')

pkgver() {
  cd "$srcdir/sgminer"
  # Use the tag of the last commit
  git describe --long | sed -E 's/([^-]*-g)/r\1/;s/-/./g'
}

prepare() {
  adlFolder="/opt/sgminer-adl-sdk"
  if [ -d ${adlFolder} ]
  then
    echo "ADL found"
    cp ${adlFolder}/*.h $srcdir/sgminer/ADL_SDK/
 else
   echo "No ADL found"
 fi
}

build() {
    cd "$srcdir/sgminer"

    git submodule init
    git submodule update
    autoreconf -i
    ./configure
    make
}

package() {
    cd "$srcdir/sgminer"
    
    mkdir -p $pkgdir/usr/bin
                  
    install -D -m755 sgminer $pkgdir/usr/bin/
    install -D -m644 kernel/*.cl $pkgdir/usr/bin/    
}
