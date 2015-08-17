# Maintainer: Nils Schäfer <nils.schaefer@gmail.com>
pkgname=syncevolution
pkgver=1.5
pkgrel=1
pkgdesc="Provides full two-way synchronization for Evolution via SyncML and ActiveSync. Templates available for Funambol, eGroupware, Memotoo, Mobical and Ovi. (no phonesync over bluetooth)"
arch=('i686' 'x86_64')
url="http://syncevolution.org/"
license=('GPL')
depends=('evolution' 'python2' 'openobex' 'libnotify' 'evolution-activesync')
optdepends=('twisted: support for running local http server')
makedepends=('autoconf' 'boost' 'docutils' 'intltool' 'cppunit' 'python-pygments')
source=(http://downloads.syncevolution.org/syncevolution/sources/$pkgname-$pkgver.tar.gz)
md5sums=('bbb59b88cb19ae0440bfe587293012eb')

build() {
  cd ${srcdir}/$pkgname-*
  #patch -p1 < ${srcdir}/0001-syncevo-dbus-server-deal-with-libnotify-0.5.x-compil.patch
  #patch -Nup1 -i ${srcdir}/gcc-4.6.patch
  CXXFLAGS+=" -fpermissive"

  ./configure --prefix=/usr \
              --enable-core \
              --enable-gui \
              --enable-dbus-service \
              --enable-gtk=2 \
              --enable-activesync
  make 
}

package(){
  cd ${srcdir}/$pkgname-*
  make DESTDIR="${pkgdir}" install
  sed -i 's/\/usr\/bin\/python/\/usr\/bin\/python2/' ${pkgdir}/usr/bin/syncevo-phone-config
  sed -i 's/\/usr\/bin\/python/\/usr\/bin\/python2/' ${pkgdir}/usr/bin/syncevo-http-server
  #install -D -m644 ${pkgdir}/usr/etc/xdg/autostart/syncevo-dbus-server.desktop ${pkgdir}/etc/xdg/autostart/syncevo-dbus-server.desktop
  rm -R ${pkgdir}/usr/etc

}
