# colab-ffmpeg-cuda

FFmpeg build with CUDA support for Linux (especially for Google Colab, updated for NVIDIA driver version `460.32.03` and CUDA version `11.2`) with pre-built binaries.

Pre-built binaries were built from scratch on *Nov. 21, 2022* using the [markus-perl /`ffmpeg-build-script`](https://github.com/markus-perl/ffmpeg-build-script) with [`nv-codec-headers`](https://github.com/FFmpeg/nv-codec-headers) version [`11.0.10.2`](https://github.com/FFmpeg/nv-codec-headers/releases/tag/n11.0.10.2) *(as newer versions `11.1` are too recent for NVIDIA driver version `460.32.03`)*.

## Set Up

**Important:** You have to change the runtime type and use GPU hardware accelerator. If you have not done it, [check it below](#change-runtime-type-hardware-accelerator):

1. Clone the repository

2. Copy all the pre-built binaries from `./colab-ffmpeg-cuda/bin/` to `/usr/bin/` (**Recommended**)

```bash
!cp -r ./colab-ffmpeg-cuda/bin/. /usr/bin/
```

3. Check the installed `ffmpeg` version

```bash
!ffmpeg -version
# Congratulations, ffmpeg with cuda support is installed!
```

### Is it not working?

These pre-built binaries were built from scratch using the [markus-perl /`ffmpeg-build-script`](https://github.com/markus-perl/ffmpeg-build-script).

If you are having trouble with the pre-built binaries, buid the binaries from scratch (**It may take up to between 50 minutes and an hour**).

```bash
!chmod +x ./colab-ffmpeg-cuda/build-ffmpeg && ./colab-ffmpeg-cuda/build-ffmpeg --build --enable-gpl-and-non-free
```

---

## Change Runtime Type (Hardware Accelerator)

1. Go to `Runtime` on top-left options

2. Then go to `Change runtime type`

3. Set `Hardware accelerator` type to `GPU`

## Supported Codecs

- `x264`: H.264 Video Codec (MPEG-4 AVC)
- `x265`: H.265 Video Codec (HEVC)
- `aom`: AV1 Video Codec (Experimental and very slow!)
- `fdk_aac`: Fraunhofer FDK AAC Codec
- `xvidcore`: MPEG-4 video coding standard
- `VP8/VP9/webm`: VP8 / VP9 Video Codec for the WebM video file format
- `mp3`: MPEG-1 or MPEG-2 Audio Layer III
- `ogg`: Free, open container format
- `vorbis`: Lossy audio compression format
- `theora`: Free lossy video compression format
- `opus`: Lossy audio coding format
- `srt`: Secure Reliable Transport
- `srt`: Secure Reliable Transport
- `webp`: Image format both lossless and lossy

### HardwareAccel

- `nv-codec`: [NVIDIA's GPU accelerated video codecs](https://devblogs.nvidia.com/nvidia-ffmpeg-transcoding-guide/). These encoders/decoders will only be available if a CUDA installation was found while building the binary. Luckily, Google Colab GPU instance comes already configured with CUDA and the pre-built binaries included in this repository were built/compiled in the same environment. Supported codecs in nvcodec:
  - Decoders
    - H264 `h264_cuvid`
    - H265 `hevc_cuvid`
    - Motion JPEG `mjpeg_cuvid`
    - MPEG1 video `mpeg1_cuvid`
    - MPEG2 video `mpeg2_cuvid`
    - MPEG4 part 2 video `mepg4_cuvid`
    - VC-1 `vc1_cuvid`
    - VP8 `vp8_cuvid`
    - VP9 `vp9_cuvid`
  - Encoders
    - H264 `nvenc_h264`
    - H265 `nvenc_hevc`

_Read more: https://github.com/markus-perl/ffmpeg-build-script_

## Video Codec SDK version 11.0.10.2 Requirements:

```
Minimum required driver versions:
Linux: 455.28 or newer
Windows: 456.71 or newer

Optional CUDA 11.x features:
Linux: 450.80.02 or newer
Windows: 452.39 or newer
```

## Nvidia Driver Details

command: `nvidia-smi`

The current build is configured according to the following driver specifications. Incase the binaries or the build is not working, cross verify the requirements and the latest driver specifications in Google Colab.

As of `Mon Nov 21 10:43:08 2022` the Nvidia driver specification in Google Colab GPU instance is:

```
Mon Nov 21 10:43:08 2022       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 460.32.03    Driver Version: 460.32.03    CUDA Version: 11.2     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Tesla T4            Off  | 00000000:00:04.0 Off |                    0 |
| N/A   48C    P8     9W /  70W |      0MiB / 15109MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
```

## Version verbose of pre-built binary
```
ffmpeg version v1.41-1-g2f934b1 Copyright (c) 2000-2022 the FFmpeg developers
built with gcc 7 (Ubuntu 7.5.0-3ubuntu1~18.04)
configuration: --enable-nonfree --enable-gpl --enable-openssl --enable-libdav1d --enable-libsvtav1 --enable-libx264 --enable-libx265 --enable-libvpx --enable-libxvid --enable-libvidstab --enable-libaom --enable-libzimg --enable-lv2 --enable-libopencore_amrnb --enable-libopencore_amrwb --enable-libmp3lame --enable-libopus --enable-libvorbis --enable-libtheora --enable-libfdk-aac --enable-libwebp --enable-libsrt --enable-cuda-nvcc --enable-cuvid --enable-nvenc --enable-cuda-llvm --enable-libnpp --nvccflags='-gencode arch=compute_52,code=sm_52' --enable-amf --disable-debug --disable-doc --disable-shared --enable-pthreads --enable-static --enable-small --enable-version3 --extra-cflags='-I/content/ffmpeg-build-script/workspace/include -I/content/ffmpeg-build-script/workspace/include/lilv-0 -I/usr/local/cuda/include' --extra-ldexeflags= --extra-ldflags='-L/content/ffmpeg-build-script/workspace/lib -L/usr/local/cuda/lib64' --extra-libs='-ldl -lpthread -lm -lz' --pkgconfigdir=/content/ffmpeg-build-script/workspace/lib/pkgconfig --pkg-config-flags=--static --prefix=/content/ffmpeg-build-script/workspace --extra-version=
libavutil      57. 28.100 / 57. 28.100
libavcodec     59. 37.100 / 59. 37.100
libavformat    59. 27.100 / 59. 27.100
libavdevice    59.  7.100 / 59.  7.100
libavfilter     8. 44.100 /  8. 44.100
libswscale      6.  7.100 /  6.  7.100
libswresample   4.  7.100 /  4.  7.100
libpostproc    56.  6.100 / 56.  6.100
```
### More Info on the build

```
C compiler                gcc
C library                 glibc
ARCH                      x86 (generic)
big-endian                no
runtime cpu detection     yes
standalone assembly       yes
x86 assembler             nasm
MMX enabled               yes
MMXEXT enabled            yes
3DNow! enabled            yes
3DNow! extended enabled   yes
SSE enabled               yes
SSSE3 enabled             yes
AESNI enabled             yes
AVX enabled               yes
AVX2 enabled              yes
AVX-512 enabled           yes
AVX-512ICL enabled        yes
XOP enabled               yes
FMA3 enabled              yes
FMA4 enabled              yes
i686 features enabled     yes
CMOV is fast              yes
EBX available             yes
EBP available             yes
debug symbols             no
strip symbols             yes
optimize for size         yes
optimizations             yes
static                    yes
shared                    no
postprocessing support    yes
network support           yes
threading support         pthreads
safe bitstream reader     yes
texi2html enabled         no
perl enabled              yes
pod2man enabled           yes
makeinfo enabled          no
makeinfo supports HTML    no
xmllint enabled           no

External libraries:
alsa                    libsrt                  libxcb_shape
bzlib                   libsvtav1               libxcb_xfixes
iconv                   libtheora               libxvid
libaom                  libvidstab              libzimg
libdav1d                libvorbis               lv2
libfdk_aac              libvpx                  lzma
libmp3lame              libwebp                 openssl
libopencore_amrnb       libx264                 sdl2
libopencore_amrwb       libx265                 zlib
libopus                 libxcb

External libraries providing hardware acceleration:
amf                     cuvid                   nvenc
cuda                    ffnvcodec               v4l2_m2m
cuda_llvm               libnpp
cuda_nvcc               nvdec

Libraries:
avcodec                 avformat                swresample
avdevice                avutil                  swscale
avfilter                postproc

Programs:
ffmpeg                  ffplay                  ffprobe

Enabled decoders:
aac                     fmvc                    pcm_vidc
aac_fixed               fourxm                  pcx
aac_latm                fraps                   pfm
aasc                    frwu                    pgm
ac3                     g2m                     pgmyuv
ac3_fixed               g723_1                  pgssub
acelp_kelvin            g729                    pgx
adpcm_4xm               gdv                     phm
adpcm_adx               gem                     photocd
adpcm_afc               gif                     pictor
adpcm_agm               gremlin_dpcm            pixlet
adpcm_aica              gsm                     pjs
adpcm_argo              gsm_ms                  png
adpcm_ct                h261                    ppm
adpcm_dtk               h263                    prores
adpcm_ea                h263_v4l2m2m            prosumer
adpcm_ea_maxis_xa       h263i                   psd
adpcm_ea_r1             h263p                   ptx
adpcm_ea_r2             h264                    qcelp
adpcm_ea_r3             h264_cuvid              qdm2
adpcm_ea_xas            h264_v4l2m2m            qdmc
adpcm_g722              hap                     qdraw
adpcm_g726              hca                     qoi
adpcm_g726le            hcom                    qpeg
adpcm_ima_acorn         hevc                    qtrle
adpcm_ima_alp           hevc_cuvid              r10k
adpcm_ima_amv           hevc_v4l2m2m            r210
adpcm_ima_apc           hnm4_video              ra_144
adpcm_ima_apm           hq_hqa                  ra_288
adpcm_ima_cunning       hqx                     ralf
adpcm_ima_dat4          huffyuv                 rasc
adpcm_ima_dk3           hymt                    rawvideo
adpcm_ima_dk4           iac                     realtext
adpcm_ima_ea_eacs       idcin                   rl2
adpcm_ima_ea_sead       idf                     roq
adpcm_ima_iss           iff_ilbm                roq_dpcm
adpcm_ima_moflex        ilbc                    rpza
adpcm_ima_mtf           imc                     rscc
adpcm_ima_oki           imm4                    rv10
adpcm_ima_qt            imm5                    rv20
adpcm_ima_rad           indeo2                  rv30
adpcm_ima_smjpeg        indeo3                  rv40
adpcm_ima_ssi           indeo4                  s302m
adpcm_ima_wav           indeo5                  sami
adpcm_ima_ws            interplay_acm           sanm
adpcm_ms                interplay_dpcm          sbc
adpcm_mtaf              interplay_video         scpr
adpcm_psx               ipu                     screenpresso
adpcm_sbpro_2           jacosub                 sdx2_dpcm
adpcm_sbpro_3           jpeg2000                sga
adpcm_sbpro_4           jpegls                  sgi
adpcm_swf               jv                      sgirle
adpcm_thp               kgv1                    sheervideo
adpcm_thp_le            kmvc                    shorten
adpcm_vima              lagarith                simbiosis_imx
adpcm_xa                libaom_av1              sipr
adpcm_yamaha            libdav1d                siren
adpcm_zork              libfdk_aac              smackaud
agm                     libopencore_amrnb       smacker
aic                     libopencore_amrwb       smc
alac                    libopus                 smvjpeg
alias_pix               libvorbis               snow
als                     libvpx_vp8              sol_dpcm
amrnb                   libvpx_vp9              sonic
amrwb                   loco                    sp5x
amv                     lscr                    speedhq
anm                     m101                    speex
ansi                    mace3                   srgc
ape                     mace6                   srt
apng                    magicyuv                ssa
aptx                    mdec                    stl
aptx_hd                 metasound               subrip
arbc                    microdvd                subviewer
argo                    mimic                   subviewer1
ass                     mjpeg                   sunrast
asv1                    mjpeg_cuvid             svq1
asv2                    mjpegb                  svq3
atrac1                  mlp                     tak
atrac3                  mmvideo                 targa
atrac3al                mobiclip                targa_y216
atrac3p                 motionpixels            tdsc
atrac3pal               movtext                 text
atrac9                  mp1                     theora
aura                    mp1float                thp
aura2                   mp2                     tiertexseqvideo
av1                     mp2float                tiff
av1_cuvid               mp3                     tmv
avrn                    mp3adu                  truehd
avrp                    mp3adufloat             truemotion1
avs                     mp3float                truemotion2
avui                    mp3on4                  truemotion2rt
ayuv                    mp3on4float             truespeech
bethsoftvid             mpc7                    tscc
bfi                     mpc8                    tscc2
bink                    mpeg1_cuvid             tta
binkaudio_dct           mpeg1_v4l2m2m           twinvq
binkaudio_rdft          mpeg1video              txd
bintext                 mpeg2_cuvid             ulti
bitpacked               mpeg2_v4l2m2m           utvideo
bmp                     mpeg2video              v210
bmv_audio               mpeg4                   v210x
bmv_video               mpeg4_cuvid             v308
brender_pix             mpeg4_v4l2m2m           v408
c93                     mpegvideo               v410
cavs                    mpl2                    vb
ccaption                msa1                    vble
cdgraphics              mscc                    vbn
cdtoons                 msmpeg4v1               vc1
cdxl                    msmpeg4v2               vc1_cuvid
cfhd                    msmpeg4v3               vc1_v4l2m2m
cinepak                 msnsiren                vc1image
clearvideo              msp2                    vcr1
cljr                    msrle                   vmdaudio
cllc                    mss1                    vmdvideo
comfortnoise            mss2                    vmnc
cook                    msvideo1                vorbis
cpia                    mszh                    vp3
cri                     mts2                    vp4
cscd                    mv30                    vp5
cyuv                    mvc1                    vp6
dca                     mvc2                    vp6a
dds                     mvdv                    vp6f
derf_dpcm               mvha                    vp7
dfa                     mwsc                    vp8
dfpwm                   mxpeg                   vp8_cuvid
dirac                   nellymoser              vp8_v4l2m2m
dnxhd                   notchlc                 vp9
dolby_e                 nuv                     vp9_cuvid
dpx                     on2avc                  vp9_v4l2m2m
dsd_lsbf                opus                    vplayer
dsd_lsbf_planar         paf_audio               vqa
dsd_msbf                paf_video               wavpack
dsd_msbf_planar         pam                     wcmv
dsicinaudio             pbm                     webp
dsicinvideo             pcm_alaw                webvtt
dss_sp                  pcm_bluray              wmalossless
dst                     pcm_dvd                 wmapro
dvaudio                 pcm_f16le               wmav1
dvbsub                  pcm_f24le               wmav2
dvdsub                  pcm_f32be               wmavoice
dvvideo                 pcm_f32le               wmv1
dxa                     pcm_f64be               wmv2
dxtory                  pcm_f64le               wmv3
dxv                     pcm_lxf                 wmv3image
eac3                    pcm_mulaw               wnv1
eacmv                   pcm_s16be               wrapped_avframe
eamad                   pcm_s16be_planar        ws_snd1
eatgq                   pcm_s16le               xan_dpcm
eatgv                   pcm_s16le_planar        xan_wc3
eatqi                   pcm_s24be               xan_wc4
eightbps                pcm_s24daud             xbin
eightsvx_exp            pcm_s24le               xbm
eightsvx_fib            pcm_s24le_planar        xface
escape124               pcm_s32be               xl
escape130               pcm_s32le               xma1
evrc                    pcm_s32le_planar        xma2
exr                     pcm_s64be               xpm
fastaudio               pcm_s64le               xsub
ffv1                    pcm_s8                  xwd
ffvhuff                 pcm_s8_planar           y41p
ffwavesynth             pcm_sga                 ylc
fic                     pcm_u16be               yop
fits                    pcm_u16le               yuv4
flac                    pcm_u24be               zero12v
flashsv                 pcm_u24le               zerocodec
flashsv2                pcm_u32be               zlib
flic                    pcm_u32le               zmbv
flv                     pcm_u8

Enabled encoders:
a64multi                huffyuv                 pcm_u8
a64multi5               jpeg2000                pcm_vidc
aac                     jpegls                  pcx
ac3                     libaom_av1              pfm
ac3_fixed               libfdk_aac              pgm
adpcm_adx               libmp3lame              pgmyuv
adpcm_argo              libopencore_amrnb       phm
adpcm_g722              libopus                 png
adpcm_g726              libsvtav1               ppm
adpcm_g726le            libtheora               prores
adpcm_ima_alp           libvorbis               prores_aw
adpcm_ima_amv           libvpx_vp8              prores_ks
adpcm_ima_apm           libvpx_vp9              qoi
adpcm_ima_qt            libwebp                 qtrle
adpcm_ima_ssi           libwebp_anim            r10k
adpcm_ima_wav           libx264                 r210
adpcm_ima_ws            libx264rgb              ra_144
adpcm_ms                libx265                 rawvideo
adpcm_swf               libxvid                 roq
adpcm_yamaha            ljpeg                   roq_dpcm
alac                    magicyuv                rpza
alias_pix               mjpeg                   rv10
amv                     mlp                     rv20
apng                    movtext                 s302m
aptx                    mp2                     sbc
aptx_hd                 mp2fixed                sgi
ass                     mpeg1video              smc
asv1                    mpeg2video              snow
asv2                    mpeg4                   sonic
avrp                    mpeg4_v4l2m2m           sonic_ls
avui                    msmpeg4v2               speedhq
ayuv                    msmpeg4v3               srt
bitpacked               msvideo1                ssa
bmp                     nellymoser              subrip
cfhd                    opus                    sunrast
cinepak                 pam                     svq1
cljr                    pbm                     targa
comfortnoise            pcm_alaw                text
dca                     pcm_bluray              tiff
dfpwm                   pcm_dvd                 truehd
dnxhd                   pcm_f32be               tta
dpx                     pcm_f32le               ttml
dvbsub                  pcm_f64be               utvideo
dvdsub                  pcm_f64le               v210
dvvideo                 pcm_mulaw               v308
eac3                    pcm_s16be               v408
exr                     pcm_s16be_planar        v410
ffv1                    pcm_s16le               vbn
ffvhuff                 pcm_s16le_planar        vc2
fits                    pcm_s24be               vorbis
flac                    pcm_s24daud             vp8_v4l2m2m
flashsv                 pcm_s24le               wavpack
flashsv2                pcm_s24le_planar        webvtt
flv                     pcm_s32be               wmav1
g723_1                  pcm_s32le               wmav2
gif                     pcm_s32le_planar        wmv1
h261                    pcm_s64be               wmv2
h263                    pcm_s64le               wrapped_avframe
h263_v4l2m2m            pcm_s8                  xbm
h263p                   pcm_s8_planar           xface
h264_amf                pcm_u16be               xsub
h264_nvenc              pcm_u16le               xwd
h264_v4l2m2m            pcm_u24be               y41p
hevc_amf                pcm_u24le               yuv4
hevc_nvenc              pcm_u32be               zlib
hevc_v4l2m2m            pcm_u32le               zmbv

Enabled hwaccels:
av1_nvdec               mpeg1_nvdec             vp8_nvdec
h264_nvdec              mpeg2_nvdec             vp9_nvdec
hevc_nvdec              mpeg4_nvdec             wmv3_nvdec
mjpeg_nvdec             vc1_nvdec

Enabled parsers:
aac                     dvbsub                  mpegvideo
aac_latm                dvd_nav                 opus
ac3                     dvdsub                  png
adx                     flac                    pnm
amr                     g723_1                  qoi
av1                     g729                    rv30
avs2                    gif                     rv40
avs3                    gsm                     sbc
bmp                     h261                    sipr
cavsvideo               h263                    tak
cook                    h264                    vc1
cri                     hevc                    vorbis
dca                     ipu                     vp3
dirac                   jpeg2000                vp8
dnxhd                   mjpeg                   vp9
dolby_e                 mlp                     webp
dpx                     mpeg4video              xbm
dvaudio                 mpegaudio               xma

Enabled demuxers:
aa                      idcin                   pcm_f64le
aac                     idf                     pcm_mulaw
aax                     iff                     pcm_s16be
ac3                     ifv                     pcm_s16le
ace                     ilbc                    pcm_s24be
acm                     image2                  pcm_s24le
act                     image2_alias_pix        pcm_s32be
adf                     image2_brender_pix      pcm_s32le
adp                     image2pipe              pcm_s8
ads                     image_bmp_pipe          pcm_u16be
adx                     image_cri_pipe          pcm_u16le
aea                     image_dds_pipe          pcm_u24be
afc                     image_dpx_pipe          pcm_u24le
aiff                    image_exr_pipe          pcm_u32be
aix                     image_gem_pipe          pcm_u32le
alp                     image_gif_pipe          pcm_u8
amr                     image_j2k_pipe          pcm_vidc
amrnb                   image_jpeg_pipe         pjs
amrwb                   image_jpegls_pipe       pmp
anm                     image_jpegxl_pipe       pp_bnk
apc                     image_pam_pipe          pva
ape                     image_pbm_pipe          pvf
apm                     image_pcx_pipe          qcp
apng                    image_pfm_pipe          r3d
aptx                    image_pgm_pipe          rawvideo
aptx_hd                 image_pgmyuv_pipe       realtext
aqtitle                 image_pgx_pipe          redspark
argo_asf                image_phm_pipe          rl2
argo_brp                image_photocd_pipe      rm
argo_cvg                image_pictor_pipe       roq
asf                     image_png_pipe          rpl
asf_o                   image_ppm_pipe          rsd
ass                     image_psd_pipe          rso
ast                     image_qdraw_pipe        rtp
au                      image_qoi_pipe          rtsp
av1                     image_sgi_pipe          s337m
avi                     image_sunrast_pipe      sami
avr                     image_svg_pipe          sap
avs                     image_tiff_pipe         sbc
avs2                    image_vbn_pipe          sbg
avs3                    image_webp_pipe         scc
bethsoftvid             image_xbm_pipe          scd
bfi                     image_xpm_pipe          sdp
bfstm                   image_xwd_pipe          sdr2
bink                    ingenient               sds
binka                   ipmovie                 sdx
bintext                 ipu                     segafilm
bit                     ircam                   ser
bitpacked               iss                     sga
bmv                     iv8                     shorten
boa                     ivf                     siff
brstm                   ivr                     simbiosis_imx
c93                     jacosub                 sln
caf                     jv                      smacker
cavsvideo               kux                     smjpeg
cdg                     kvag                    smush
cdxl                    live_flv                sol
cine                    lmlm4                   sox
codec2                  loas                    spdif
codec2raw               lrc                     srt
concat                  luodat                  stl
data                    lvf                     str
daud                    lxf                     subviewer
dcstr                   m4v                     subviewer1
derf                    matroska                sup
dfa                     mca                     svag
dfpwm                   mcc                     svs
dhav                    mgsts                   swf
dirac                   microdvd                tak
dnxhd                   mjpeg                   tedcaptions
dsf                     mjpeg_2000              thp
dsicin                  mlp                     threedostr
dss                     mlv                     tiertexseq
dts                     mm                      tmv
dtshd                   mmf                     truehd
dv                      mods                    tta
dvbsub                  moflex                  tty
dvbtxt                  mov                     txd
dxa                     mp3                     ty
ea                      mpc                     v210
ea_cdata                mpc8                    v210x
eac3                    mpegps                  vag
epaf                    mpegts                  vc1
ffmetadata              mpegtsraw               vc1t
filmstrip               mpegvideo               vividas
fits                    mpjpeg                  vivo
flac                    mpl2                    vmd
flic                    mpsub                   vobsub
flv                     msf                     voc
fourxm                  msnwc_tcp               vpk
frm                     msp                     vplayer
fsb                     mtaf                    vqf
fwse                    mtv                     w64
g722                    musx                    wav
g723_1                  mv                      wc3
g726                    mvi                     webm_dash_manifest
g726le                  mxf                     webvtt
g729                    mxg                     wsaud
gdv                     nc                      wsd
genh                    nistsphere              wsvqa
gif                     nsp                     wtv
gsm                     nsv                     wv
gxf                     nut                     wve
h261                    nuv                     xa
h263                    obu                     xbin
h264                    ogg                     xmv
hca                     oma                     xvag
hcom                    paf                     xwma
hevc                    pcm_alaw                yop
hls                     pcm_f32be               yuv4mpegpipe
hnm                     pcm_f32le
ico                     pcm_f64be

Enabled muxers:
a64                     h263                    pcm_s16le
ac3                     h264                    pcm_s24be
adts                    hash                    pcm_s24le
adx                     hds                     pcm_s32be
aiff                    hevc                    pcm_s32le
alp                     hls                     pcm_s8
amr                     ico                     pcm_u16be
amv                     ilbc                    pcm_u16le
apm                     image2                  pcm_u24be
apng                    image2pipe              pcm_u24le
aptx                    ipod                    pcm_u32be
aptx_hd                 ircam                   pcm_u32le
argo_asf                ismv                    pcm_u8
argo_cvg                ivf                     pcm_vidc
asf                     jacosub                 psp
asf_stream              kvag                    rawvideo
ass                     latm                    rm
ast                     lrc                     roq
au                      m4v                     rso
avi                     matroska                rtp
avif                    matroska_audio          rtp_mpegts
avm2                    md5                     rtsp
avs2                    microdvd                sap
avs3                    mjpeg                   sbc
bit                     mkvtimestamp_v2         scc
caf                     mlp                     segafilm
cavsvideo               mmf                     segment
codec2                  mov                     smjpeg
codec2raw               mp2                     smoothstreaming
crc                     mp3                     sox
dash                    mp4                     spdif
data                    mpeg1system             spx
daud                    mpeg1vcd                srt
dfpwm                   mpeg1video              stream_segment
dirac                   mpeg2dvd                streamhash
dnxhd                   mpeg2svcd               sup
dts                     mpeg2video              swf
dv                      mpeg2vob                tee
eac3                    mpegts                  tg2
f4v                     mpjpeg                  tgp
ffmetadata              mxf                     truehd
fifo                    mxf_d10                 tta
fifo_test               mxf_opatom              ttml
filmstrip               null                    uncodedframecrc
fits                    nut                     vc1
flac                    obu                     vc1t
flv                     oga                     voc
framecrc                ogg                     w64
framehash               ogv                     wav
framemd5                oma                     webm
g722                    opus                    webm_chunk
g723_1                  pcm_alaw                webm_dash_manifest
g726                    pcm_f32be               webp
g726le                  pcm_f32le               webvtt
gif                     pcm_f64be               wsaud
gsm                     pcm_f64le               wtv
gxf                     pcm_mulaw               wv
h261                    pcm_s16be               yuv4mpegpipe

Enabled protocols:
async                   httpproxy               rtmpt
cache                   https                   rtmpte
concat                  icecast                 rtmpts
concatf                 ipfs                    rtp
crypto                  ipns                    srtp
data                    libsrt                  subfile
ffrtmpcrypt             md5                     tcp
ffrtmphttp              mmsh                    tee
file                    mmst                    tls
ftp                     pipe                    udp
gopher                  prompeg                 udplite
gophers                 rtmp                    unix
hls                     rtmpe
http                    rtmps

Enabled filters:
abench                  dblur                   pad
abitscope               dcshift                 pal100bars
acompressor             dctdnoiz                pal75bars
acontrast               deband                  palettegen
acopy                   deblock                 paletteuse
acrossfade              decimate                pan
acrossover              deconvolve              perms
acrusher                dedot                   perspective
acue                    deesser                 phase
addroi                  deflate                 photosensitivity
adeclick                deflicker               pixdesctest
adeclip                 dejudder                pixelize
adecorrelate            delogo                  pixscope
adelay                  derain                  pp
adenorm                 deshake                 pp7
aderivative             despill                 premultiply
adrawgraph              detelecine              prewitt
adynamicequalizer       dialoguenhance          pseudocolor
adynamicsmooth          dilation                psnr
aecho                   displace                pullup
aemphasis               dnn_classify            qp
aeval                   dnn_detect              random
aevalsrc                dnn_processing          readeia608
aexciter                doubleweave             readvitc
afade                   drawbox                 realtime
afftdn                  drawgraph               remap
afftfilt                drawgrid                removegrain
afifo                   drmeter                 removelogo
afir                    dynaudnorm              repeatfields
afirsrc                 earwax                  replaygain
aformat                 ebur128                 reverse
afreqshift              edgedetect              rgbashift
afwtdn                  elbg                    rgbtestsrc
agate                   entropy                 roberts
agraphmonitor           epx                     rotate
ahistogram              eq                      sab
aiir                    equalizer               scale
aintegral               erosion                 scale2ref
ainterleave             estdif                  scale2ref_npp
alatency                exposure                scale_cuda
alimiter                extractplanes           scale_npp
allpass                 extrastereo             scdet
allrgb                  fade                    scharr
allyuv                  feedback                scroll
aloop                   fftdnoiz                segment
alphaextract            fftfilt                 select
alphamerge              field                   selectivecolor
amerge                  fieldhint               sendcmd
ametadata               fieldmatch              separatefields
amix                    fieldorder              setdar
amovie                  fifo                    setfield
amplify                 fillborders             setparams
amultiply               find_rect               setpts
anequalizer             firequalizer            setrange
anlmdn                  flanger                 setsar
anlmf                   floodfill               settb
anlms                   format                  sharpen_npp
anoisesrc               fps                     shear
anull                   framepack               showcqt
anullsink               framerate               showfreqs
anullsrc                framestep               showinfo
apad                    freezedetect            showpalette
aperms                  freezeframes            showspatial
aphasemeter             fspp                    showspectrum
aphaser                 gblur                   showspectrumpic
aphaseshift             geq                     showvolume
apsyclip                gradfun                 showwaves
apulsator               gradients               showwavespic
arealtime               graphmonitor            shuffleframes
aresample               grayworld               shufflepixels
areverse                greyedge                shuffleplanes
arnndn                  guided                  sidechaincompress
asdr                    haas                    sidechaingate
asegment                haldclut                sidedata
aselect                 haldclutsrc             sierpinski
asendcmd                hdcd                    signalstats
asetnsamples            headphone               signature
asetpts                 hflip                   silencedetect
asetrate                highpass                silenceremove
asettb                  highshelf               sinc
ashowinfo               hilbert                 sine
asidedata               histeq                  siti
asoftclip               histogram               smartblur
aspectralstats          hqdn3d                  smptebars
asplit                  hqx                     smptehdbars
astats                  hstack                  sobel
astreamselect           hsvhold                 spectrumsynth
asubboost               hsvkey                  speechnorm
asubcut                 hue                     split
asupercut               huesaturation           spp
asuperpass              hwdownload              sr
asuperstop              hwmap                   ssim
atadenoise              hwupload                stereo3d
atempo                  hwupload_cuda           stereotools
atilt                   hysteresis              stereowiden
atrim                   identity                streamselect
avectorscope            idet                    super2xsai
avgblur                 il                      superequalizer
avsynctest              inflate                 surround
axcorrelate             interlace               swaprect
bandpass                interleave              swapuv
bandreject              join                    tblend
bass                    kerndeint               telecine
bbox                    kirsch                  testsrc
bench                   lagfun                  testsrc2
bilateral               latency                 thistogram
biquad                  lenscorrection          threshold
bitplanenoise           life                    thumbnail
blackdetect             limitdiff               thumbnail_cuda
blackframe              limiter                 tile
blend                   loop                    tiltshelf
blockdetect             loudnorm                tinterlace
blurdetect              lowpass                 tlut2
bm3d                    lowshelf                tmedian
boxblur                 lumakey                 tmidequalizer
bwdif                   lut                     tmix
cas                     lut1d                   tonemap
cellauto                lut2                    tpad
channelmap              lut3d                   transpose
channelsplit            lutrgb                  transpose_npp
chorus                  lutyuv                  treble
chromahold              lv2                     tremolo
chromakey               mandelbrot              trim
chromakey_cuda          maskedclamp             unpremultiply
chromanr                maskedmax               unsharp
chromashift             maskedmerge             untile
ciescope                maskedmin               v360
codecview               maskedthreshold         vaguedenoiser
color                   maskfun                 varblur
colorbalance            mcompand                vectorscope
colorchannelmixer       median                  vflip
colorchart              mergeplanes             vfrdet
colorcontrast           mestimate               vibrance
colorcorrect            metadata                vibrato
colorhold               midequalizer            vidstabdetect
colorize                minterpolate            vidstabtransform
colorkey                mix                     vif
colorlevels             monochrome              vignette
colormap                morpho                  virtualbass
colormatrix             movie                   vmafmotion
colorspace              mpdecimate              volume
colorspectrum           mptestsrc               volumedetect
colortemperature        msad                    vstack
compand                 multiply                w3fdif
compensationdelay       negate                  waveform
concat                  nlmeans                 weave
convolution             nnedi                   xbr
convolve                noformat                xcorrelate
copy                    noise                   xfade
cover_rect              normalize               xmedian
crop                    null                    xstack
cropdetect              nullsink                yadif
crossfeed               nullsrc                 yadif_cuda
crystalizer             oscilloscope            yaepblur
cue                     overlay                 yuvtestsrc
curves                  overlay_cuda            zoompan
datascope               owdenoise               zscale

Enabled bsfs:
aac_adtstoasc           h264_redundant_pps      opus_metadata
av1_frame_merge         hapqa_extract           pcm_rechunk
av1_frame_split         hevc_metadata           pgs_frame_merge
av1_metadata            hevc_mp4toannexb        prores_metadata
chomp                   imx_dump_header         remove_extradata
dca_core                mjpeg2jpeg              setts
dump_extradata          mjpega_dump_header      text2movsub
dv_error_marker         mov2textsub             trace_headers
eac3_core               mp3_header_decompress   truehd_core
extract_extradata       mpeg2_metadata          vp9_metadata
filter_units            mpeg4_unpack_bframes    vp9_raw_reorder
h264_metadata           noise                   vp9_superframe
h264_mp4toannexb        null                    vp9_superframe_split

Enabled indevs:
alsa                    lavfi                   v4l2
fbdev                   oss                     xcbgrab

Enabled outdevs:
alsa                    oss                     v4l2
fbdev                   sdl2
```

---

_original project: https://github.com/markus-perl/ffmpeg-build-script_

_Please visit the original repo, modify it according to your needs_
