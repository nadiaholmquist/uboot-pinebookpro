# U-Boot: Pinebook Pro based on PKGBUILD for Rock64
# Maintainer: Dan Johansen <strit@manjaro.org>
# Contributor: Kevin Mihelich 
# Contributor: Adam <adam900710@gmail.com>

pkgname=uboot-pinebookpro
pkgver=2020.01
pkgrel=7
pkgdesc="U-Boot for Pinebook Pro"
arch=('aarch64')
url='https://git.eno.space/pbp-uboot.'
license=('GPL')
backup=('etc/conf.d/mkextlinuxconf')
makedepends=('git' 'arm-none-eabi-gcc' 'dtc' 'bc')
install=${pkgname}.install
_tfa_tag=v2.3
source=("git+https://git.eno.space/pbp-uboot.git"
        "git+https://github.com/ARM-software/arm-trusted-firmware.git#tag=$_tfa_tag"
        "mkextlinuxconf" "pinebookpro.conf")
sha256sums=('SKIP'
            'SKIP'
            'd229a6ae07cb95ac92da52f9740b8659c016ac53f150e38dce5db5550bdce8cd'
            '8eeaa66ef7dcd7a134b8afe613eb0b0fd72c77d90c0dddff93a703af64d328d4')

prepare() {
  cd pbp-uboot
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
  install -d "${pkgdir}/boot/extlinux"
  install -Dm644 pbp-uboot/idbloader.img "${pkgdir}/boot/idbloader.img"
  install -Dm644 pbp-uboot/u-boot.itb "${pkgdir}/boot/u-boot.itb"
  install -Dm644 pinebookpro.conf "${pkgdir}/etc/conf.d/mkextlinuxconf"
  install -Dm755 mkextlinuxconf "${pkgdir}/usr/bin/mkextlinuxconf"
}
