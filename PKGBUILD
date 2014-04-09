# Maintainer: Artur Sobierak <asobierak@gmail.com>

pkgname=aceorb
pkgver=6.2.5
pkgrel=1
pkgdesc="C++ CORBA implementation"
arch=('i686' 'x86_64')
url="http://www.cs.wustl.edu/~schmidt/TAO.html"
license=('Other')
groups=('base-devel')
depends=('glibc')
source=(http://download.dre.vanderbilt.edu/previous_versions/ACE+TAO-${pkgver}.tar.gz)
md5sums=('e40e1a0320312b24136496b525cd50e2')

build() {
  cd "$srcdir"/ACE_wrappers
  
  export ACE_ROOT="$srcdir"/ACE_wrappers
  export TAO_ROOT=$ACE_ROOT/TAO
  export LD_LIBRARY_PATH=$ACE_ROOT/lib:$LD_LIBRARY_PATH

  echo "#include \"$ACE_ROOT/ace/config-linux.h\"" > $ACE_ROOT/ace/config.h
  echo "include \$(ACE_ROOT)/include/makeinclude/platform_linux.GNU" > $ACE_ROOT/include/makeinclude/platform_macros.GNU
  echo "INSTALL_PREFIX=/usr" >> $ACE_ROOT/include/makeinclude/platform_macros.GNU
  #echo "TAO_ORBSVCS=CosNaming" >> $ACE_ROOT/include/makeinclude/platform_macros.GNU
  #echo "TAO_ORBSVCS=CosNaming CosTrading RTEvent Security RTSched PortableGroup FTORB_Utils FtRtEvent CosLoadBalancing CosNotification_MC" >> $ACE_ROOT/include/makeinclude/platform_macros.GNU
 
  cd $ACE_ROOT/ace && make -j8
  cd $ACE_ROOT/apps/gperf/src && make -j8
  cd $TAO_ROOT/TAO_IDL && make -j8
  cd $TAO_ROOT/tao && make -j8
  cd $TAO_ROOT/orbsvcs && make -j8 
}

package() {
  cd "$srcdir"/ACE_wrappers
  
  export ACE_ROOT="$srcdir"/ACE_wrappers
  export TAO_ROOT=$ACE_ROOT/TAO
  export LD_LIBRARY_PATH=$ACE_ROOT/lib:$LD_LIBRARY_PATH
  
  cd $ACE_ROOT/ace && make -j8 DESTDIR="$pkgdir" install
  cd $ACE_ROOT/apps/gperf/src && make -j8 DESTDIR="$pkgdir" install
  cd $TAO_ROOT/TAO_IDL && make -j8 DESTDIR="$pkgdir" install
  cd $TAO_ROOT/tao && make -j8 DESTDIR="$pkgdir" install
  cd $TAO_ROOT/orbsvcs && make -j8 DESTDIR="$pkgdir" install
  
  echo "#include \"/usr/include/ace/config-linux.h\"" > $pkgdir/usr/include/ace/config.h
}

