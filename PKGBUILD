# Maintainer: Merlin Attila Fejzuli <merlin@fejzuli.com>
pkgname=lockgame3d
pkgver=1.0
pkgrel=1
epoch=0
pkgdesc="Realistic lockpicking game"
arch=('x86_64')
url="http://theamazingking.com/lockgame.php"
license=('CCPL')
depends=('glibc' 'libglvnd' 'glu' 'libx11' 'sdl12-compat')
makedepends=('gzip')
source=("$pkgname-$pkgver.tar.gz::http://theamazingking.com/lockgame/linuxLockGameSrc.tar.gz"
        "lock-font_and_model_fix.diff"
        "$pkgname.6")
noextract=("$pkgname-$pkgver.tar.gz")
sha256sums=('3aca8426b58128c4586ebde7a59ac230418b0f5677909499d59ff6aa8aa2c3a5'
            'ede3114f33aad61c5506d6f14fc8c2f2bc8ad9b007d1efa669d2c07afd3ae6c2'
            '6fbcacb6b018fc69b33eeabd68429027a1bcd0b28cc63b93ea67f195aefd6ffa')

prepare() {
    mkdir -p "$pkgname-$pkgver"
    tar -xf "$pkgname-$pkgver.tar.gz" -C "$pkgname-$pkgver"
    patch -uN "$pkgname-$pkgver/lock.c" lock-font_and_model_fix.diff || return 1
}

build() {
    cd "$pkgname-$pkgver"
    gcc lock.c -o "$pkgname" -lm -lGL -lGLU `pkg-config --cflags --libs x11` `sdl-config --cflags --libs` -z relro -z now
}

package() {
	cd "$pkgname-$pkgver"
    mkdir -p "$pkgdir/usr/bin" "$pkgdir/usr/share/$pkgname" "$pkgdir/usr/share/man/man6"
    install "$pkgname" "$pkgdir/usr/bin"
    install arrow.obj \
            betterplug.obj \
            bogotacontour.obj \
            bogota.obj \
            deforestcontour.obj \
            deforest.obj \
            halfcontour.obj \
            halfdiamond.obj \
            hook2.obj \
            hookcontour.obj \
            longcontour.obj \
            long.obj \
            pin.obj \
            reachcontour.obj \
            reachpick.obj \
            serrated.obj \
            shell.obj \
            snakecontour.obj \
            snake.obj \
            spool.obj \
            spoorated.obj \
            spring.obj \
            tension.obj \
            topin.obj \
            "$pkgdir/usr/share/$pkgname"
    gzip -c "$srcdir/$pkgname.6" > "$pkgname.6.gz"
    install "$pkgname.6.gz" "$pkgdir/usr/share/man/man6"
}
