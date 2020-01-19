# U-Boot: Pinebook Pro based on PKGBUILD for Rock64
# Maintainer: Dan Johansen <strit@manjaro.org>
# Contributor: Kevin Mihelich 
# Contributor: Adam <adam900710@gmail.com>

pkgname=uboot-pinebookpro
pkgver=2020.01
pkgrel=3
pkgdesc="U-Boot for Pinebook Pro"
arch=('aarch64')
url='https://git.eno.space/pbp-uboot.'
license=('GPL')
backup=('boot/boot.txt' 'boot/boot.scr')
depends=('uboot-tools')
makedepends=('git' 'arm-none-eabi-gcc' 'dtc' 'bc')
install=${pkgname}.install
_commit_atf=22d12c4148c373932a7a81e5d1c59a767e143ac2
source=("git+https://git.eno.space/pbp-uboot.git"
        "git+https://github.com/ARM-software/arm-trusted-firmware.git#commit=$_commit_atf"
        #'0001-nvme-support.patch'
        'boot.txt'
        'mkscr')
sha256sums=('SKIP'
            'SKIP'
            'e88152627854a5c70ee68403330da8e4637251954acd2c59c4a06ba3cea8f4fa'
            'a4fc8b6b92bc364d6542670d294aa618a8501fb8729f415cc0a3eed776ef0c8e')

prepare() {
  cd pbp-uboot
  #patch -Np1 -i "${srcdir}/0001-nvme-support.patch"
}

build() {
  cd arm-trusted-firmware
  unset CFLAGS CXXFLAGS CPPFLAGS LDFLAGS
  make PLAT=rk3399
  cd ../pbp-uboot
  unset CFLAGS CXXFLAGS CPPFLAGS LDFLAGS
  make pinebook_pro-rk3399_defconfig
  echo 'CONFIG_IDENT_STRING=" Manjaro ARM"' >> .config
  #echo 'CONFIG_PCIE_ROCKCHIP=y' >> .config
  make BL31=../arm-trusted-firmware/build/rk3399/release/bl31/bl31.elf EXTRAVERSION=-${pkgrel}
}

package() {
  cd pbp-uboot

  mkdir -p "${pkgdir}/boot"
  cp idbloader.img u-boot.itb  "${pkgdir}/boot"
  mkimage -A arm -O linux -T script -C none -n "U-Boot boot script" -d ../boot.txt "${pkgdir}/boot/boot.scr"
  cp ../{boot.txt,mkscr} "${pkgdir}"/boot
}
