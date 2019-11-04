# U-Boot: Pinebook Pro
# Maintainer: Dan Johansen <strit@manjaro.org>
# Contributor: Spikerguy <tech@fkardame.com>
# Pre-Built IMG by MrFixit

pkgname=uboot-pinebookpro
pkgver=1.1
pkgrel=3
pkgdesc="U-Boot for Pinebook Pro (prebuilt binaries)"
arch=('aarch64')
url='https://github.com/mrfixit2001/updates_repo/tree/v1.1/pinebook/filesystem'
license=('GPL')
makedepends=('uboot-tools')
#Commented out until we know the parition to be used.
#install=${pkgname}.install
source=('uboot.img'
    'trust.img'
	'idbloader.img'
	'boot.txt'
	'mkscr'
        )
md5sums=('e073aa1f531e666fc4e8678e8ffaa016'
         '2ad66a3fc90823e48fdd081059543709'
         '763b41dbc3fee4aaf26b720e7722b235'
         '1a91a14854f5eac2b50dd4267cc877ef'
         '021623a04afd29ac3f368977140cfbfd')

package() {
  mkdir -p "${pkgdir}"/boot
  cp uboot.img trust.img idbloader.img "${pkgdir}"/boot
  mkimage -A arm -O linux -T script -C none -n "U-Boot boot script" -d ../boot.txt "${pkgdir}/boot/boot.scr"
  cp ../{boot.txt,mkscr} "${pkgdir}"/boot
}
 
