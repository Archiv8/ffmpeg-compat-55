# Maintainer: Muflone http://www.muflone.com/contacts/english/

pkgname=ffmpeg-compat-55
pkgver=2.3.6
pkgrel=4
pkgdesc="Compatibility package for ffmpeg to provide versions 55 of libavcodec, libavdevice and libavformat, not anymore provided by the ffmpeg package"
arch=(
  "i686"
  "x86_64"
)
url="http://ffmpeg.org/"
license=(
  "GPL"
)
depends=(
  "gsm"
  "lame"
  "opencore-amr"
  "openjpeg"
  "opus"
  "rtmpdump"
  "libvpx"
  "schroedinger"
  "speex"
  "v4l-utils"
  "xvidcore"
  "libpulse"
  "libtheora"
  "libbluray"
  "libmodplug"
  "libva"
  "libxv"
  "sdl"
  "jack"
  "libavutil-52"
)
makedepends=(
  "yasm"
  "libass"
)
provides=(
  "libavcodec.so"
  "libavdevice.so"
  "libavformat.so"
)
source=(
  "http://ffmpeg.org/releases/ffmpeg-${pkgver}.tar.bz2"
  "http://ffmpeg.org/releases/ffmpeg-${pkgver}.tar.bz2.asc"
  "libvpx_VP8E_UPD_ENTROPY.patch"::"https://git.videolan.org/?p=ffmpeg.git;a=commitdiff_plain;h=6540fe04a3f9a11ba7084a49b3ee5fa2fc5b32ab"
)
sha512sums=(
  "8f46648ae54edc5a57d2a120d60aa84ad7f9631986bf9b63a7650467322164756dc3bf3f677a4c250331fd2dbc4db002e2bdbfa3e4561397532267b46f15c2fe"
  "SKIP"
  "39c2fc65a521c0dbc421a706b81c534e0ffa802f03a8f11a84eefe716ddefca64ca0741c3de3df4d9e1ad9a2658d2daa5bfb28817efbe72f979fc6854951364e"
)
options=(

  # Add !lto to options to prevent build failure
  "!lto"
)
validpgpkeys=(
  "FCF986EA15E6E293A5644F10B4322F04D67658D8"
)

prepare() {

  cd "ffmpeg-${pkgver}"

  patch -p1 -i "../libvpx_VP8E_UPD_ENTROPY.patch"
}

build() {

  cd "ffmpeg-${pkgver}"

  ./configure \
    --prefix=/usr \
    --incdir="/usr/include" \
    --shlibdir="/usr/lib" \
    --libdir="/usr/lib" \
    --disable-debug \
    --disable-static \
    --enable-dxva2 \
    --disable-fontconfig \
    --enable-gpl \
    --enable-libass \
    --enable-libbluray \
    --enable-libfreetype \
    --enable-libgsm \
    --enable-libmodplug \
    --enable-libmp3lame \
    --enable-libopencore_amrnb \
    --enable-libopencore_amrwb \
    --enable-libopenjpeg \
    --enable-libopus \
    --enable-libpulse \
    --enable-librtmp \
    --enable-libschroedinger \
    --enable-libspeex \
    --enable-libtheora \
    --enable-libv4l2 \
    --enable-libvorbis \
    --enable-libvpx \
    --disable-libx264 \
    --enable-libxvid \
    --enable-runtime-cpudetect \
    --enable-shared \
    --enable-vdpau \
    --enable-version3 \
    --enable-x11grab \
    --disable-doc \
    --disable-programs \
    --disable-avresample \
    --disable-avfilter \
    --disable-postproc \
    --disable-swresample \
    --disable-swscale

  make
}

package() {

  cd "ffmpeg-${pkgver}"

  make DESTDIR="${pkgdir}" install-libs

  cd "${pkgdir}/usr/lib"

  rm -f *.so libavutil.*
}
