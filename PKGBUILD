# U-Boot: Pinebook Pro based on PKGBUILD for Rock64
# Maintainer: Dan Johansen <strit@manjaro.org>
# Contributor: Kevin Mihelich 
# Contributor: Adam <adam900710@gmail.com>

pkgname=uboot-pinebookpro
pkgver=2017.09
pkgrel=2
pkgdesc="U-Boot for Pinebook Pro - MrFixit2001's source tree"
arch=('aarch64')
url='http://www.denx.de/wiki/U-Boot/WebHome'
license=('GPL')
backup=('boot/boot.txt' 'boot/boot.scr')
depends=('uboot-tools')
makedepends=('bc' 'git' 'rockchip-tools' 'python' 'dtc')
install=${pkgname}.install
_commit_rkbin=0d4740f2c0c897ebc1a074580376689b8454ddd8
_commit_uboot=183e247f9022f934a2224ce71f3030447068c32c
source=("git+https://github.com/mrfixit2001/rockchip-u-boot.git#commit=$_commit_uboot"
        "git+https://github.com/rockchip-linux/rkbin.git#commit=$_commit_rkbin"
        "0001-nvme-support.patch"
        'rk3399trust.ini'
        'boot.txt'
        'mkscr')
sha256sums=('SKIP'
            'SKIP'
            '35e36df708fef1dbb9b1335b527e9b38f58479d07073ebb44379950204255ab4'
            'c83b2423355a6c3e29f8d2ea8aa9ebc1c75b15d635500546ce9dc64faef3f1ce'
            'e88152627854a5c70ee68403330da8e4637251954acd2c59c4a06ba3cea8f4fa'
            'a4fc8b6b92bc364d6542670d294aa618a8501fb8729f415cc0a3eed776ef0c8e')
prepare() {
  cd rockchip-u-boot
  patch -Np1 -i "${srcdir}/0001-nvme-support.patch"
  sed -i 's/KBUILD_CFLAGS	+= -fshort-wchar -Werror/KBUILD_CFLAGS	+= -fshort-wchar/' Makefile
}
  
build() {
  cd rockchip-u-boot

  unset CLFAGS CXXFLAGS CPPFLAGS LDFLAGS

  make pinebookpro-rk3399_defconfig
  sed -i 's/CONFIG_IDENT_STRING=""/CONFIG_IDENT_STRING=" Manjaro ARM"/' .config
  make EXTRAVERSION=-${pkgrel}
}

package() {
  cd rockchip-u-boot

  mkdir -p "${pkgdir}/boot"

  tools/mkimage -n rk3399 -T rksd -d ../rkbin/bin/rk33/rk3399_ddr_800MHz_v1.23.bin "${pkgdir}/boot/idbloader.img"
  cat ../rkbin/bin/rk33/rk3399_miniloader_v1.19.bin >> "${pkgdir}/boot/idbloader.img"

  loaderimage --pack --uboot u-boot-dtb.bin "${pkgdir}/boot/uboot.img" 0x200000

  trust_merger ../rk3399trust.ini

  cp trust.img "${pkgdir}/boot"

  tools/mkimage -A arm -O linux -T script -C none -n "U-Boot boot script" -d ../boot.txt "${pkgdir}/boot/boot.scr"
  cp ../{boot.txt,mkscr} "${pkgdir}"/boot
}
