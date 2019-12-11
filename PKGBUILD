# U-Boot: Pinebook Pro
# Maintainer: Dan Johansen <strit@manjaro.org>
# Contributor: Spikerguy <tech@fkardame.com>
# Pre-Built IMG by MrFixit

pkgname=uboot-pinebookpro
pkgver=1.5
pkgrel=1
pkgdesc="U-Boot for Pinebook Pro (prebuilt binaries)"
arch=('aarch64')
url='https://github.com/mrfixit2001/updates_repo/tree/v1.5/pinebook/filesystem'
license=('GPL')
makedepends=('uboot-tools')
install=${pkgname}.install
source=('uboot.img'
    'trust.img'
	'idbloader.img'
	'boot.txt'
	'mkscr'
        )
md5sums=('80c927ad86428f65f4a3d1c3e846b6c8'
         '2ad66a3fc90823e48fdd081059543709'
         '763b41dbc3fee4aaf26b720e7722b235'
         '38dba847a2ca94e18509f9aaa708289d'
         '021623a04afd29ac3f368977140cfbfd')

package() {
  mkdir -p "${pkgdir}"/boot
  cp uboot.img trust.img idbloader.img "${pkgdir}"/boot
  mkimage -A arm -O linux -T script -C none -n "U-Boot boot script" -d ../boot.txt "${pkgdir}/boot/boot.scr"
  cp ../{boot.txt,mkscr} "${pkgdir}"/boot
}
 
