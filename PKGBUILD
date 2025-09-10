# Maintainer: wjsoj <wjs@wjsphy.top>

pkgname=lobe-chat-appimage
pkgver=1.126.3
pkgrel=1
pkgdesc="An open-source, modern-design LLMs/AI chat framework (AppImage)"
arch=(x86_64)
url="https://github.com/lobehub/lobe-chat"

license=('Apache-2.0')

# AppImages need fuse2 at runtime
depends=(fuse2)
conflicts=(lobe-chat)
options=(!strip)

# Upstream release asset naming (Beta channel). Adjust here if channel changes.
_channel=Beta
_upstream_base="LobeHub-${_channel}"
_appimage="${_upstream_base}-${pkgver}.AppImage"

source=("${_appimage}::${url}/releases/download/v${pkgver}/${_upstream_base}-${pkgver}.AppImage"
  "LICENSE::https://raw.githubusercontent.com/lobehub/lobe-chat/v${pkgver}/LICENSE"
  "lobe-chat.png::https://raw.githubusercontent.com/lobehub/lobe-chat/v${pkgver}/apps/desktop/resources/tray.png")

# These placeholders are auto-updated by the GitHub Actions workflow.
sha256sums=('APPIMAGE_SHA256'
            'LICENSE_SHA256'
            'ICON_SHA256')

_install_dir="opt/${pkgname}"
_exec_name="lobe-chat" # Symlink /usr/bin/lobe-chat -> AppImage

prepare() {
  # Nothing to prepare; placeholder kept for future extraction logic if needed.
  true
}

package() {
  cd "${srcdir}"

  install -Dm755 "${_appimage}" "${pkgdir}/${_install_dir}/${_exec_name}.AppImage"
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  # Install upstream tray icon as application icon 
  install -Dm644 lobe-chat.png "${pkgdir}/usr/share/icons/hicolor/64x64/apps/lobe-chat.png"

  # Basic desktop entry
  install -d "${pkgdir}/usr/share/applications"
  cat > "${pkgdir}/usr/share/applications/${pkgname}.desktop" <<EOF
[Desktop Entry]
Name=LobeChat
Comment=${pkgdesc}
Exec=${_exec_name} %u
Terminal=false
Type=Application
Categories=Network;Chat;AI;Utility;
StartupNotify=true
Icon=lobe-chat
EOF
}
