# Maintainer: SummerSad <hauvipapro@gmail.com>

pkgname=slstatus-git
pkgver=r517.8c8091f
pkgrel=1
pkgdesc='A status monitor for window managers.'
arch=('x86_64')
url='http://tools.suckless.org/slstatus'
license=('custom:ISC')
depends=('libx11')
makedepends=('git')
_patches=("config.patch")
source=("git+https://git.suckless.org/${pkgname%-git}"
	"${_patches[@]}"
)
sha256sums=('SKIP'
            '099f512c17363776d7a4dc45927bfcc82e4d6fd3013cb9f8edf3d9804cad912e')

pkgver() {
	cd "${pkgname%-git}"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
	cd "${pkgname%-git}"
	# patch
	for file in "${_patches[@]}"; do
		if [[ "$file" == *.diff || "$file" == *.patch ]]; then
			echo "Applying patch $(basename $file)..."
			patch -Np1 <"../$(basename ${file})"
		fi
	done
}

build() {
	cd "${pkgname%-git}"
	make X11INC='/usr/include/X11' X11LIB='/usr/lib/X11'
}

package() {
	cd "${pkgname%-git}"
	make DESTDIR="${pkgdir}" PREFIX='/usr/' install
	install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname%-git}/LICENSE"
	install -Dm644 README "${pkgdir}/usr/share/doc/${pkgname%-git}/README"
}
