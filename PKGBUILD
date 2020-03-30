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
backup=('boot/extlinux/extlinux.conf')
makedepends=('git' 'arm-none-eabi-gcc' 'dtc' 'bc')
install=${pkgname}.install
_commit_atf=22d12c4148c373932a7a81e5d1c59a767e143ac2
source=("git+https://git.eno.space/pbp-uboot.git"
        "git+https://github.com/ARM-software/arm-trusted-firmware.git#commit=$_commit_atf"
        "extlinux.conf")
        #'0001-nvme-support.patch')
sha256sums=('SKIP'
            'SKIP'
            'e29431ffeb7368983c74b7f7ea108f74e1363305231b0b5bb698884945ab0c5a')

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

  mkdir -p "${pkgdir}/boot/extlinux"
  cp idbloader.img u-boot.itb  "${pkgdir}/boot"
  cp "${srcdir}"/extlinux.conf "${pkgdir}"/boot/extlinux
}
