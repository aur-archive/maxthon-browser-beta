# Maintainer: Maxthon Inc. <maxthon AT maxthon a-dot net>
# Maintainer: dongfengweixiao <dongfengweixiao at gmail a-dot com>

pkgname=maxthon-browser-beta
pkgver=1.0.5.3
pkgrel=1
pkgdesc="A browser that combines a minimal design with sophisticated technology to make the web faster, safer, and easier.(Beta Channel)"
arch=('i686' 'x86_64')
url="http://www.maxthon.cn/"
license=('Custom')
depends=('libxrandr' 'libxrender' 'libxss' 'libxext' 'glibc' 'glib2' 'atk' 'pango' 'gdk-pixbuf2' 'cairo' 'freetype2' 'fontconfig' 'nss' 'nspr' 'gconf' 'dbus' 'libxcomposite' 'alsa-lib' 'libxdamage' 'libxfixes' 'libcups' 'libgcrypt15' 'expat' 'gcc-libs' 'pcre' 'libffi' 'libxinerama' 'libxi' 'libxcursor' 'harfbuzz' 'libpng' 'pixman' 'zlib' 'bzip2' 'dbus-glib' 'krb5' 'e2fsprogs' 'gnutls' 'avahi' 'libgpg-error' 'libxau' 'libxdmcp' 'graphite' 'libx11' 'wayland' 'mesa' 'systemd' 'libdrm' 'libxcb' 'libxxf86vm' 'keyutils' 'p11-kit' 'libtasn1' 'nettle' 'gmp' 'gtkhotkey')
options=('!emptydirs' '!strip')
provides=("maxthon-browser=$pkgver")
conflicts=('maxthon-browser')
install=$pkgname.install

_arch=i386
[ "$CARCH" = 'x86_64' ] && _arch=amd64
  source=("${pkgname}_${pkgver}_${_arch}.deb::http://dl.maxthon.cn/linux/deb/packages/${_arch}/${pkgname}_${pkgver}_${_arch}.deb")
	md5sums=('d5b232f37f5ebee7d1d6a54279225cee')
[ "$CARCH" = 'x86_64' ] && md5sums[0]='29bb5c5721d90d2ec728fc904a95ec82'

package() {
  msg2 "Extracting the data.lzma"
  bsdtar -xf data.tar.lzma -C "$pkgdir/"
  install -dm755 "$pkgdir"/usr/share/applications/
  
  msg2 "Setting sandbox system permissions"
  chown root:root "$pkgdir"/opt/maxthon/maxthon_sandbox
  chmod 4755 "$pkgdir"/opt/maxthon/maxthon_sandbox
  
  msg2 "Registered the icon resource & desktop file"
  for i in 22 24 32 48 64 128 256; do
  install -Dm644 "$pkgdir"/opt/maxthon/product_logo_${i}.png "$pkgdir"/usr/share/icons/hicolor/${i}x${i}/apps/maxthon-browser.png
  done
  mv "$pkgdir"/opt/maxthon/maxthon.desktop "$pkgdir"/usr/share/applications/maxthon.desktop

  install -dm755 "$pkgdir"/etc/default/maxthon.d/
  cat "$pkgdir"/opt/maxthon/conf.d/pn > "$pkgdir"/etc/default/maxthon.d/pn
  
  msg2 "Symlinking missing Udev lib"
  ln -s /usr/lib/libudev.so.1 "$pkgdir"/opt/maxthon/libudev.so.0
  
  #if [ $(pacman -Q libgcrypt | cut -d " " -f2 | tr -d .-) -ge 1601 ]; then
  #msg2 "Installing compatible Gcrypt lib"
  #install -m755 "$startdir"/libgcrypt-$CARCH.so.11 "$pkgdir"/opt/maxthon/libgcrypt.so.11
  #fi
  
  msg2 "Removing the duplicated images"
  rm "$pkgdir"/opt/maxthon/product_logo_*.png
}
