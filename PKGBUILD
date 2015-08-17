# Maintainer: damkrat <akm47c@gmail.com>
# Contributor: Imanol Celaya <ornitorrincos@archlinux-es.org>
# Contributor: Lukas Jirkovsky <l.jirkovsky@gmail.com>
# Contributor: Dan Vratil <progdan@progdansoft.com>
# Contributor: thotypous <matiasΘarchlinux-br·org>
# Contributor: delor <bartekpiech gmail com>

pkgname=qt4creator
pkgver=3.1.81
pkgrel=1
pkgdesc='Lightweight, cross-platform integrated development environment (Built with Qt4, clang and libc++)'
arch=('i686' 'x86_64')
url='http://qt-project.org'
license=('LGPL')
depends=('qt4-clang' 'clang')
makedepends=('git' 'mesa' 'clang')
options=('docs')
optdepends=('gdb: for the debugger'
            'cmake: for cmake project support'
            'openssh-askpass: for ssh support'
            'git: for git support'
            'mercurial: for mercurial support'
            'bzr: for bazaar support'
            'clang: Clang code model'
            'valgrind: for analyze support')

install=qt4creator.install

source=('git://gitorious.org/qt-creator/qt-creator.git'
        'git://gitorious.org/qt-labs/qbs.git'
        'qt4creator.desktop'
				'qt4creator')
md5sums=('SKIP'
         'SKIP'
         '7ea16e1d13bfbfa8c4af824523b19f01'
				 '9639b11ecaf831f00847361c9a4b0c80')

_mkspec=linux-clang

prepare() {
  cd qt-creator
  git submodule init
  git config submodule.qbs.url $srcdir/qbs
  git submodule update
}

build() {
  [[ -d qtbuild ]] && rm -rf qtbuild
  mkdir qtbuild && cd qtbuild

  LLVM_INSTALL_DIR=/usr qmake-qt4-clang -r -spec $_mkspec ../qt-creator/qtcreator.pro

	make
	make docs
}

package() {
  cd qtbuild

  make INSTALL_ROOT="${pkgdir}/opt/qt4creator/" install
  make INSTALL_ROOT="${pkgdir}/opt/qt4creator/" install_docs

	install -d "${pkgdir}"/usr/bin
		#ln -s "/opt/qt4creator/bin/qtcreator" "${pkgdir}"/usr/bin/qt4creator
		cp "${srcdir}"/qt4creator  "${pkgdir}"/usr/bin/  	

	install -d "${pkgdir}"/usr/share/icons
		cp -Rf "${pkgdir}"/opt/qt4creator/share/icons/* "${pkgdir}"/usr/share/icons 
		rm -Rf "${pkgdir}"/opt/qt4creator/share/icons

	install -Dm644 ${srcdir}/qt4creator.desktop ${pkgdir}/usr/share/applications/qt4creator.desktop
  install -Dm644 ${srcdir}/qt-creator/LGPL_EXCEPTION.TXT ${pkgdir}/usr/share/licenses/qt4creator/LGPL_EXCEPTION.TXT
}
