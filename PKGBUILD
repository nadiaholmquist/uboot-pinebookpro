# U-Boot: Pinebook Pro
# Maintainer: Spikerguy <tech@fkardame.com>
# Pre-Built IMG by MrFixit

buildarch=8

pkgname=uboot-pinebookpro
pkgver=1.1
pkgrel=1
pkgdesc="U-Boot for Pinebook Pro"
arch=('aarch64')
url='https://github.com/mrfixit2001/updates_repo/tree/v1.1/pinebook/filesystem'
license=('GPL')
#makedepends=( )
install=${pkgname}.install
source=('uboot.img'
        'trust.img'
	'idbloader.img'
        )
md5sums=('e073aa1f531e666fc4e8678e8ffaa016'
         '2ad66a3fc90823e48fdd081059543709'
         '763b41dbc3fee4aaf26b720e7722b235'
         )

#pkgver() {
#  cd u-boot
#  git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
#}

package() {
  mkdir -p "${pkgdir}"/boot
  cp uboot.img trust.img idbloader.img "${pkgdir}"/boot
}
 
