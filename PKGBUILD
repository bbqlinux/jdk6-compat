# Maintainer: Daniel Hillenbrand <codeworkx [at] bbqlinux [dot] org>
# Shamelessly stolen from:
# "jre6" & "jdk6" Maintainer: Ethan Hall
# "jre6" & "jdk6" Contributors: Guillaume ALAUX, Daniel J Griffiths, Jason Chu, Geoffroy Carrier, Thomas Dziedzic, Dan Serban

pkgname=jdk6-compat
pkgver=6u51
pkgrel=09
epoch=2
pkgdesc="Java 6 Development Kit designed to work alongside OpenJDK7 installation"
url=http://www.oracle.com/technetwork/java/javase/downloads/index.html
arch=(i686 x86_64)
license=(custom)
depends=(jre6-compat)
makedepends=(lynx)
replaces=(sun-jdk6,j2sdk)
#DLAGENTS=('http::/usr/bin/curl -fLC - --retry 3 --retry-delay 3 -o %o %u --header "Cookie:oraclelicensejdk-${pkgver}-oth-JPR=accept-securebackup-cookie;gpw_e24=http://edelivery.oracle.com"')
DLAGENTS=('http::/usr/bin/curl -LC - -b "oraclelicense=a" -O') 
install=jdk.install
source=("http://download.oracle.com/otn-pub/java/jdk/$pkgver-b$pkgrel/jdk-$pkgver-linux-i586.bin"
				'java-control-panel.desktop'
        'java-monitoring-and-management-console.desktop'
        'java-policy-settings.desktop'
        'java-visualvm.desktop'
        'java-web-start.desktop'
        'jdk6.profile'
        'jdk6.profile.csh'
        'construct.sh'
        'derby-network-server'
        'derby-network-server.conf')

md5sums=('ab18c2e0244f09dff0d49a328ebe5775'
         'e4d814c0f310d77ed6990c731bccd0fb'
         '4bc2b0be93f76ed07b471e3c89eb5a8a'
         '8e3cec7ab641ec449cabd068be583f5c'
         '9ba148ebabce8ed3351b813a9a66b6e5'
         '619ec32235dcfe454234ef4316f8a7cc'
         '39239a4b3296971ac6fd9a8df25e4107'
         '8aaa7219aa62d4c344e828d71003344d'
         '70b34ef3d5b997e7c15b1b50053d3e37'
         'a279e195e249000646895d93e199860d'
         '4bdff6982c66d24a879c424aaac3d04d')
_arch=i586
[ "${CARCH}" == 'x86_64' ] && _arch=x64

[ "$CARCH" == 'x86_64' ] && source[0]="http://download.oracle.com/otn-pub/java/jdk/$pkgver-b$pkgrel/jdk-$pkgver-linux-x64.bin" && md5sums[0]='81e97879481bf32e9af63206b121e6f2'

package()
{

  rm -rf unbundle-jdk
  mkdir unbundle-jdk
  cd unbundle-jdk
  
  sh ../jdk-$pkgver-linux-$_arch.bin -noregister
  
  cd ..
	
  sh construct.sh unbundle-jdk linux-jdk linux-jre
  
  rm -rf linux-jdk/jre
  
  mkdir -p "${pkgdir}"/usr/lib/jvm/java-6-oracle/
  mv linux-jdk/* "${pkgdir}"/usr/lib/jvm/java-6-oracle/

  mkdir -p "${pkgdir}"/usr/share/licenses/jdk6-oracle
  install -m644 "${pkgdir}"/usr/lib/jvm/java-6-oracle/COPYRIGHT "${pkgdir}"/usr/share/licenses/jdk6-oracle
  install -m644 "${pkgdir}"/usr/lib/jvm/java-6-oracle/LICENSE "${pkgdir}"/usr/share/licenses/jdk6-oracle
  install -m644 "${pkgdir}"/usr/lib/jvm/java-6-oracle/THIRDPARTYLICENSEREADME.txt "${pkgdir}"/usr/share/licenses/jdk6-oracle

}

