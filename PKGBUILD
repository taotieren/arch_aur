# Maintainer: taotieren <admin@taotieren.com>

pkgname=ksa-linux
pkgver=0.80
pkgrel=1
#epoch=0
pkgdesc="Kanxue Security Access"
arch=('i686' 'x86_64' 'armv7h' 'aarch64' )
license=('unknow')
#groups=('')
depends=('unzip')
#source_x86_64=("KSA_${pkgver}_linux_x86_64.zip::KSA_${pkgver}_linux.zip")
#source_i686=("KSA_${pkgver}_linux_i686.zip::KSA_${pkgver}_linux.zip")
#source_armv7h=("KSA_${pkgver}_linux_arm.zip::KSA_${pkgver}_linux.zip")
#source_aarch64=("KSA_${pkgver}_linux_arm64.zip::KSA_${pkgver}_linux.zip")

source=("KSA_${pkgver}_linux.zip")
#desktops=("ksa-linux.desktop")
#source+=(${desktops[@]})
#sha256sums_i686=('b4cafff1b7ee02ec404ca784d8605d4d61f7fdc4551baebb56cbaa08770359ce')
#sha256sums_x86_64=('b4cafff1b7ee02ec404ca784d8605d4d61f7fdc4551baebb56cbaa08770359ce')
#sha256sums_armv7h=('b4cafff1b7ee02ec404ca784d8605d4d61f7fdc4551baebb56cbaa08770359ce')
#sha256sums_aarch64=('b4cafff1b7ee02ec404ca784d8605d4d61f7fdc4551baebb56cbaa08770359ce')

sha256sums=("b4cafff1b7ee02ec404ca784d8605d4d61f7fdc4551baebb56cbaa08770359ce")

#install=$pkgname.install
url="https://bbs.pediy.com/thread-252417.htm"
conflicts=("ksa-linux")
replaces=("ksa-linux")
#DLAGENTS=("https::/usr/bin/env curl -o %o -d accept_license_agreement=accepted -d non_emb_ctr=confirmed")
options=(!strip)

# prepare() {
#     #Change src path name
#     if [ ${CARCH} = "i686" ]; then
#         mv KSA_${pkgver}_linux_i686 KSA
#     fi
#     if [ ${CARCH} = "x86_64" ]; then
#         mv KSA_${pkgver}_linux_x86_64 KSA
#     fi
#     if [ ${CARCH} = "armv7h" ]; then
#         mv KSA_${pkgver}_linux_arm KSA
#     fi
#     if [ ${CARCH} = "aarch64" ]; then
#        mv KSA_${pkgver}_linux_arm64 KSA
#     fi
# }

package(){
    # Match package placement from their .deb, in /opt
    install -dm755 "${pkgdir}/opt/KSA" \
            "${pkgdir}/usr/bin/" \
            "${pkgdir}/usr/share/pixmaps" \
            "${pkgdir}/usr/share/applications"

    # Install desktop entry
#     for i in "${desktops[@]}"
#     do
#         install -Dm644 "${i}" "${pkgdir}/usr/share/applications/"
#     done
#     install -Dm644 "ksa.svg" "${pkgdir}/usr/share/pixmaps/ksa.svg"

    cd "${srcdir}/KSA_linux"
    cp --preserve=mode -r ksa.conf "${pkgdir}/opt/KSA"

    # Bulk copy everything
    if [ ${CARCH} = "armv7h" ]; then
        install -Dm755 ksa_arm "${pkgdir}/opt/KSA/ksa"
    elif [ ${CARCH} = "aarch64" ]; then
        install -Dm755 ksa_arm64 "${pkgdir}/opt/KSA/ksa"
    elif [ ${CARCH} = "x86_64" ]; then
        install -Dm755 ksa_x64 "${pkgdir}/opt/KSA/ksa"
    else install -Dm755 ksa_x86 "${pkgdir}/opt/KSA/ksa"
    fi

    for f in ksa; do
        ln -sf /opt/KSA/"$f" "${pkgdir}/usr/bin"
    done

}
