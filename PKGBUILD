# Maintainer: Yurii Kolesnykov <root@yurikoles.com>
# based on aur electron8-bin: Tom Vincent <http://tlvince.com/contact/>

_projectname=electron
_major=13
_pkgname="${_projectname}${_major}"
_pkgver=13.0.0-beta.7
pkgname="$_pkgname-bin"
pkgver="${_pkgver/-/.}"
pkgrel=1
pkgdesc="Build cross platform desktop apps with web technologies - version ${_major} - binary version"
arch=('x86_64' 'i686' 'armv7h' 'aarch64')
url="https://${_projectname}js.org/"
license=('MIT')
provides=("$_pkgname")
conflicts=("$_pkgname")
depends=('c-ares' 'ffmpeg' 'gtk3' 'http-parser' 'libevent' 'libxslt' 'libxss' 'minizip' 'nss' 're2' 'snappy')
optdepends=(
	'kde-cli-tools: file deletion support (kioclient5)'
	'libappindicator-gtk3: StatusNotifierItem support'
	'trash-cli: file deletion support (trash-put)'
	"xdg-utils: open URLs with desktop's default (xdg-email, xdg-open)"
)
_releaseurl="https://github.com/$_projectname/$_projectname/releases/download/v$_pkgver"
source_x86_64=(
	"$pkgname-chromedriver-$_pkgver-$pkgrel-x86_64.zip::$_releaseurl/chromedriver-v$_pkgver-linux-x64.zip"
	"$pkgname-$_pkgver-$pkgrel-x86_64.zip::$_releaseurl/$_projectname-v$_pkgver-linux-x64.zip"
)
source_i686=(
	"$pkgname-chromedriver-$_pkgver-$pkgrel-i686.zip::$_releaseurl/chromedriver-v$_pkgver-linux-ia32.zip"
	"$pkgname-$_pkgver-$pkgrel-i686.zip::$_releaseurl/$_projectname-v$_pkgver-linux-ia32.zip"
)
source_armv7h=(
	"$pkgname-chromedriver-$_pkgver-$pkgrel-armv7h.zip::$_releaseurl/chromedriver-v$_pkgver-linux-armv7l.zip"
	"$pkgname-$_pkgver-$pkgrel-armv7h.zip::$_releaseurl/$_projectname-v$_pkgver-linux-armv7l.zip"
)
source_aarch64=(
	"$pkgname-chromedriver-$_pkgver-$pkgrel-aarch64.zip::$_releaseurl/chromedriver-v$_pkgver-linux-arm64.zip"
	"$pkgname-$_pkgver-$pkgrel-aarch64.zip::$_releaseurl/$_projectname-v$_pkgver-linux-arm64.zip"
)
sha256sums_x86_64=('b0cf0ceca21874ac9821612fc70d2e4a53fe063048f97f82ee678e0c34d48296'
                   'c4218bdf967fc8a0b7133ccfac739509541ca64138790dd8773b84d27b300bca')
sha256sums_i686=('e5fc6a513d6d7fb6a02540fe9690925cb0e91c28996e99dc495290633b078e6f'
                 'd00237d6fb0f0931866dcf1ec0ae89bda3e469aa37c75901de9efd5a8a34a46b')
sha256sums_armv7h=('dfb8f4f7b3ec42bed097b681c89d35c347d37e88a903e626291893ef73aa070b'
                   'ac30caa28844576824c58ad9da27e0432a5621e4811dbef0eda8db9bfb8bf883')
sha256sums_aarch64=('62fbed7a0fd712a1f8185ce386171194e5d9150640f255fb62989e8a9697475a'
                    '68e1cdc145e9b903c457eaf0a8a914a0e61ed537916d4d7b6a3f3aaaa7d767ec')

package() {
	cd "$srcdir/"
	install -dm755 "$pkgdir/usr/lib/$_pkgname/"
	find . -mindepth 1 -maxdepth 1 -type f ! -name "*.zip" ! -name "LICENSE*" -exec cp -r --no-preserve=ownership --preserve=mode -t "$pkgdir/usr/lib/$_pkgname/." {} +

	for _folder in 'locales' 'resources' 'swiftshader'; do
		cp -r --no-preserve=ownership --preserve=mode "$_folder/" "$pkgdir/usr/lib/$_pkgname/$_folder/"
	done

	chmod u+s "$pkgdir/usr/lib/$_pkgname/chrome-sandbox"

	install -dm755 "$pkgdir/usr/bin"
	ln -nfs "/usr/lib/$_pkgname/$_projectname" "$pkgdir/usr/bin/$_pkgname"

	for _license in 'LICENSE' 'LICENSES.chromium.html'; do
		install -Dm644 "$_license" "$pkgdir/usr/share/licenses/$pkgname/$_license"
	done
}