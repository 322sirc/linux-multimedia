## Look inside 'choose-gcc-optimization.sh' to choose your microarchitecture
## Valid numbers between: 0 to 99
## Default is: 0 => generic
## Good option if your package is for one machine: 98 (Intel native) or 99 (AMD native)
_microarchitecture=47

## Major kernel version
_major=6.0
## Minor kernel version
_minor=9

## PKGBUILD ##

pkgbase=linux-multimedia
#pkgver=${_major}
pkgver=${_major}.${_minor}
pkgrel=2
pkgdesc='Linux Multimedia Optimized'
url="https://www.kernel.org/"
arch=(x86_64)
license=(GPL2)
makedepends=(
  bc kmod libelf pahole cpio perl tar xz
  xmlto python-sphinx python-sphinx_rtd_theme graphviz imagemagick
  git
)
options=('!strip')
_srcname=linux-${pkgver}
source=(
  https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-${pkgver}.tar.{xz,sign}
  "git+https://github.com/graysky2/kernel_compiler_patch.git"
  "git+https://github.com/Frogging-Family/linux-tkg.git"
  "choose-gcc-optimization.sh"
  "config"
        '0001-PCI-DPC-Quirk-poot-port-PIO-log-size-for-certain-Int.patch'
        '0002-ACPICA-include-acpi-acpixf.h-Fix-indentation.patch'
        '0003-ACPICA-Allow-address_space_handler-Install-and-_REG-.patch'
        '0004-ACPI-EC-Fix-EC-address-space-handler-unregistration.patch'
        '0005-ACPI-EC-fix-ECDT-probe-ordering-issues.patch'
        '0006-Add-IdeaPad-WMI-Fn-Keys-driver.patch'
        '0007-Add-IdeaPad-Usage-Mode-driver.patch'
        '0008-Add-IdeaPad-quick_charge-attribute-to-sysfs.patch'        
        '0009-ALSA-hda-realtek-Add-quirk-for-Yoga-devices.patch'
        '0010-HID-hid-sensor-custom-More-custom-iio-sensors.patch'
        '0011-IIO-hid-sensor-als-Use-generic-usage.patch'
)
validpgpkeys=(
  'ABAF11C65A2970B130ABE3C479BE3E4300411886'  # Linus Torvalds
  '647F28654894E3BD457199BE38DBBDC86092693E'  # Greg Kroah-Hartman
  'A2FF3A36AAA56654109064AB19802F8B0D70FC30'  # Jan Alexander Steffens (heftig)
  'C7E7849466FE2358343588377258734B41C31549'  # David Runge <dvzrv@archlinux.org>
)
sha256sums=('6114a208e82739b4a1ab059ace35262be2a83be34cd1ae23cb8a09337db831c7'
            'SKIP'
            'SKIP'
            'SKIP'
            '1ac18cad2578df4a70f9346f7c6fccbb62f042a0ee0594817fdef9f2704904ee'
            'c62b823685b3507699ca24188bfa4b904ee6444f4f75b2c771a47b1a75253213'
            'b19a23d37f3c74aa928c5d577f4fb41f115dbe1acdc3f6383ac9a53c15dbcf71'
            '2d3d2630f70455665508f1fafe9ed4a320b7e35f6c33843934f5823d175d89f7'
            '0db4eca1b2c5e75de40de2f58aefe337d236b7bb450c111ee4ca7fa460c7ee73'
            'a7a7aa38aa21d4749994c0d12823638bf83070bcdd11fb470ecd5904c5c183bf'
            '244678444eb5a297badcfedaac324d1186a8973aea0e8a98128b65eb9ecd644b'
            'c6f778d786fbdd3483c66d834321c788b2818828003862d5a2a12f4cbc1694e6'
            'c9420129ecdbdfaf3b2006923763d1291f9031f26911219910593b33b621e18d'
            'c5ade2a167b1337e5564e49f9bec135d40b30b2442174598c354d80580a0af4e'
            '4ccf87491541cd991fbb2cf05f87fd08ddb885144f7c3bc04fe16e406327b136'
            'd1b2c9c17b0c193d3df1184d0f7fc850daf9e3d84d1d34385c8a9ee10a6ae17c'
            '7ff6d9c2da686f3331c117d2f06f6aa9f37be5ac95eb781b54491e0ece517a8a')

export KBUILD_BUILD_HOST=archlinux
export KBUILD_BUILD_USER=$pkgbase
export KBUILD_BUILD_TIMESTAMP="$(date -Ru${SOURCE_DATE_EPOCH:+d @$SOURCE_DATE_EPOCH})"

prepare() {
  cd $_srcname

  echo "Setting version..."
  scripts/setlocalversion --save-scmversion
  echo "-$pkgrel" > localversion.10-pkgrel
  echo "${pkgbase#linux}" > localversion.20-pkgname
  
  ## --- Patches
  
  ### Apply patches
  msg2 "Apply Linux TKG Patches..."
  patch -Np1 < ${srcdir}/linux-tkg/linux-tkg-patches/${_major}/0001-add-sysctl-to-disallow-unprivileged-CLONE_NEWUSER-by.patch
  patch -Np1 < ${srcdir}/linux-tkg/linux-tkg-patches/${_major}/0001-mm-Support-soft-dirty-flag-reset-for-VA-range.patch
  patch -Np1 < ${srcdir}/linux-tkg/linux-tkg-patches/${_major}/0002-clear-patches.patch
  patch -Np1 < ${srcdir}/linux-tkg/linux-tkg-patches/${_major}/0002-mm-Support-soft-dirty-flag-read-with-reset.patch
  patch -Np1 < ${srcdir}/linux-tkg/linux-tkg-patches/${_major}/0003-glitched-base.patch
  patch -Np1 < ${srcdir}/linux-tkg/linux-tkg-patches/${_major}/0003-glitched-cfs.patch
  patch -Np1 < ${srcdir}/linux-tkg/linux-tkg-patches/${_major}/0003-glitched-cfs-additions.patch
  patch -Np1 < ${srcdir}/linux-tkg/linux-tkg-patches/${_major}/0006-add-acs-overrides_iommu.patch
  patch -Np1 < ${srcdir}/linux-tkg/linux-tkg-patches/${_major}/0007-v${_major}-fsync1_via_futex_waitv.patch
  patch -Np1 < ${srcdir}/linux-tkg/linux-tkg-patches/${_major}/0007-v${_major}-winesync.patch
  patch -Np1 < ${srcdir}/linux-tkg/linux-tkg-patches/${_major}/0008-${_major}-bcachefs.patch
  #patch -Np1 < ${srcdir}/linux-tkg/linux-tkg-patches/${_major}/0010-lru_${_major}.patch
  patch -Np1 < ${srcdir}/linux-tkg/linux-tkg-patches/${_major}/0012-misc-additions.patch
  patch -Np1 < ${srcdir}/linux-tkg/linux-tkg-patches/${_major}/0013-optimize_harder_O3.patch
  patch -Np1 < ${srcdir}/0001-PCI-DPC-Quirk-poot-port-PIO-log-size-for-certain-Int.patch
  patch -Np1 < ${srcdir}/0002-ACPICA-include-acpi-acpixf.h-Fix-indentation.patch
  patch -Np1 < ${srcdir}/0003-ACPICA-Allow-address_space_handler-Install-and-_REG-.patch
  patch -Np1 < ${srcdir}/0004-ACPI-EC-Fix-EC-address-space-handler-unregistration.patch
  patch -Np1 < ${srcdir}/0005-ACPI-EC-fix-ECDT-probe-ordering-issues.patch
  patch -Np1 < ${srcdir}/0006-Add-IdeaPad-WMI-Fn-Keys-driver.patch
  patch -Np1 < ${srcdir}/0007-Add-IdeaPad-Usage-Mode-driver.patch
  patch -Np1 < ${srcdir}/0008-Add-IdeaPad-quick_charge-attribute-to-sysfs.patch
  patch -Np1 < ${srcdir}/0009-ALSA-hda-realtek-Add-quirk-for-Yoga-devices.patch 
  patch -Np1 < ${srcdir}/0010-HID-hid-sensor-custom-More-custom-iio-sensors.patch
  patch -Np1 < ${srcdir}/0011-IIO-hid-sensor-als-Use-generic-usage.patch 

  msg2 "Apply GCC Optimization Patch..."
  patch -Np1 < ${srcdir}/kernel_compiler_patch/more-uarches-for-kernel-5.17+.patch

  ### Setting config
  echo "Setting config..."
  cp ${srcdir}/config .config
  make olddefconfig

  # Let's user choose microarchitecture optimization in GCC
  sh ${srcdir}/choose-gcc-optimization.sh $_microarchitecture

  ## --- Configs And Tweaks

  msg2 "Disable NUMA..."
  scripts/config --disable CONFIG_NUMA
  
  msg2 "Disable old dynticks..."
  scripts/config --disable CONFIG_NO_HZ

  msg2 "Set up a GCC -O3 optimized kernel..."
  scripts/config --disable CONFIG_CC_OPTIMIZE_FOR_PERFORMANCE
  scripts/config --enable CONFIG_CC_OPTIMIZE_FOR_PERFORMANCE_O3

  msg2 "Set tick rate to 1000HZ..."
  scripts/config --disable CONFIG_HZ_300
  scripts/config --enable CONFIG_HZ_1000
  scripts/config --set-val CONFIG_HZ 1000

  msg2 "Set default CPU governor to performance..."
  scripts/config --disable CONFIG_CPU_FREQ_DEFAULT_GOV_SCHEDUTIL
  scripts/config --disable CONFIG_CPU_FREQ_DEFAULT_GOV_POWERSAVE
  scripts/config --disable CONFIG_CPU_FREQ_DEFAULT_GOV_USERSPACE
  scripts/config --enable CONFIG_CPU_FREQ_DEFAULT_GOV_PERFORMANCE

  
  msg2 "Disable kernel debugging for smaller builds..."
  scripts/config --disable CONFIG_CONTEXT_TRACKING
  scripts/config --disable CONFIG_CONTEXT_TRACKING_FORCE
  scripts/config --disable CONFIG_DEBUG_KERNEL
  scripts/config --disable CONFIG_DEBUG_INFO
  scripts/config --disable CONFIG_UNUSED_SYMBOLS
  scripts/config --disable CONFIG_DEBUG_FS
  scripts/config --disable CONFIG_KGDB
  scripts/config --disable CONFIG_FUNCTION_TRACER
  scripts/config --disable CONFIG_STACK_TRACER
  
  
  ### Use Nconfig to customize compile options
  #make nconfig

  make -s kernelrelease > version
  echo "Prepared $pkgbase version $(<version)"
}

build() {
  cd $_srcname
  make -j$(nproc) all
}

_package() {
  pkgdesc="The $pkgdesc kernel and modules"
  depends=(coreutils kmod initramfs)
  optdepends=('wireless-regdb: to set the correct wireless channels of your country'
              'linux-firmware: firmware images needed for some devices')
  provides=(VIRTUALBOX-GUEST-MODULES WIREGUARD-MODULE)
  replaces=(virtualbox-guest-modules-mainline wireguard-mainline)

  cd $_srcname
  local kernver="$(<version)"
  local modulesdir="$pkgdir/usr/lib/modules/$kernver"

  echo "Installing boot image..."
  # systemd expects to find the kernel here to allow hibernation
  # https://github.com/systemd/systemd/commit/edda44605f06a41fb86b7ab8128dcf99161d2344
  install -Dm644 "$(make -s image_name)" "$modulesdir/vmlinuz"

  # Used by mkinitcpio to name the kernel
  echo "$pkgbase" | install -Dm644 /dev/stdin "$modulesdir/pkgbase"

  echo "Installing modules..."
  make INSTALL_MOD_PATH="$pkgdir/usr" INSTALL_MOD_STRIP=1 modules_install

  # remove build and source links
  rm "$modulesdir"/{source,build}
}

_package-headers() {
  pkgdesc="Headers and scripts for building modules for the $pkgdesc kernel"
  depends=(pahole)

  cd $_srcname
  local builddir="$pkgdir/usr/lib/modules/$(<version)/build"

  echo "Installing build files..."
  install -Dt "$builddir" -m644 .config Makefile Module.symvers System.map \
    localversion.* version vmlinux
  install -Dt "$builddir/kernel" -m644 kernel/Makefile
  install -Dt "$builddir/arch/x86" -m644 arch/x86/Makefile
  cp -t "$builddir" -a scripts

  # required when STACK_VALIDATION is enabled
  install -Dt "$builddir/tools/objtool" tools/objtool/objtool

  echo "Installing headers..."
  cp -t "$builddir" -a include
  cp -t "$builddir/arch/x86" -a arch/x86/include
  install -Dt "$builddir/arch/x86/kernel" -m644 arch/x86/kernel/asm-offsets.s

  install -Dt "$builddir/drivers/md" -m644 drivers/md/*.h
  install -Dt "$builddir/net/mac80211" -m644 net/mac80211/*.h

  # https://bugs.archlinux.org/task/13146
  install -Dt "$builddir/drivers/media/i2c" -m644 drivers/media/i2c/msp3400-driver.h

  # https://bugs.archlinux.org/task/20402
  install -Dt "$builddir/drivers/media/usb/dvb-usb" -m644 drivers/media/usb/dvb-usb/*.h
  install -Dt "$builddir/drivers/media/dvb-frontends" -m644 drivers/media/dvb-frontends/*.h
  install -Dt "$builddir/drivers/media/tuners" -m644 drivers/media/tuners/*.h

  # https://bugs.archlinux.org/task/71392
  install -Dt "$builddir/drivers/iio/common/hid-sensors" -m644 drivers/iio/common/hid-sensors/*.h

  echo "Installing KConfig files..."
  find . -name 'Kconfig*' -exec install -Dm644 {} "$builddir/{}" \;

  echo "Removing unneeded architectures..."
  local arch
  for arch in "$builddir"/arch/*/; do
    [[ $arch = */x86/ ]] && continue
    echo "Removing $(basename "$arch")"
    rm -r "$arch"
  done

  echo "Removing documentation..."
  rm -r "$builddir/Documentation"

  echo "Removing broken symlinks..."
  find -L "$builddir" -type l -printf 'Removing %P\n' -delete

  echo "Removing loose objects..."
  find "$builddir" -type f -name '*.o' -printf 'Removing %P\n' -delete

  echo "Stripping build tools..."
  local file
  while read -rd '' file; do
    case "$(file -bi "$file")" in
      application/x-sharedlib\;*)      # Libraries (.so)
        strip -v $STRIP_SHARED "$file" ;;
      application/x-archive\;*)        # Libraries (.a)
        strip -v $STRIP_STATIC "$file" ;;
      application/x-executable\;*)     # Binaries
        strip -v $STRIP_BINARIES "$file" ;;
      application/x-pie-executable\;*) # Relocatable binaries
        strip -v $STRIP_SHARED "$file" ;;
    esac
  done < <(find "$builddir" -type f -perm -u+x ! -name vmlinux -print0)

  echo "Stripping vmlinux..."
  strip -v $STRIP_STATIC "$builddir/vmlinux"

  echo "Adding symlink..."
  mkdir -p "$pkgdir/usr/src"
  ln -sr "$builddir" "$pkgdir/usr/src/$pkgbase"
}

pkgname=("$pkgbase" "$pkgbase-headers")
for _p in "${pkgname[@]}"; do
  eval "package_$_p() {
    $(declare -f "_package${_p#$pkgbase}")
    _package${_p#$pkgbase}
  }"
done

# vim:set ts=8 sts=2 sw=2 et:
