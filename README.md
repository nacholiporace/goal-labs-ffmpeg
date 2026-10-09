# FFmpeg para Goal Labs

Builds de FFmpeg que lleva [Goal Labs](https://goallabs.com.ar), la aplicación de escritorio de análisis de video de fútbol, y el código fuente que corresponde a cada uno.

Goal Labs ejecuta FFmpeg como un programa separado. FFmpeg se distribuye bajo la **GNU Lesser General Public License, versión 2.1 o posterior** (LGPL 2.1+). Este repositorio cumple la oferta de código fuente de esa licencia: cada release trae el binario exacto que viaja con la aplicación, su hash SHA-256 y el código fuente de FFmpeg y de las bibliotecas que lleva compiladas.

## Qué hay en cada release

| Archivo | Qué es |
|---|---|
| `ffmpeg-<versión>-win64-lgpl-shared.zip` | `ffmpeg.exe`, `ffprobe.exe` y las DLL que necesitan (Windows x64). Incluye `LICENSE.txt`, `version.json` (configuración, licencia, lista de DLL) y `SOURCES.md` (bibliotecas, versiones, licencias y de dónde sale cada una) |
| `ffmpeg-<versión>-win64-lgpl-shared.zip.sha256` | Hash del zip |
| `ffmpeg-<versión>-win64-sources.zip` | Código fuente de FFmpeg (tarball oficial de ffmpeg.org con su firma) y de las bibliotecas externas de ese build |
| `ffmpeg-<versión>-darwin-arm64.tar.gz` | El build de Mac (Apple Silicon), cuando esté publicado |

## Cómo se compila

Los builds los generan dos workflows públicos del repositorio privado de Goal Labs, que se reproducen con las mismas versiones:

- Windows: `.github/workflows/ffmpeg-windows.yml`. MSYS2 (MINGW64), tarball oficial de ffmpeg.org con firma verificada, `--disable-gpl --disable-nonfree`, sin `--enable-version3`, y solo lo que usa la aplicación: Media Foundation, DirectShow, Schannel, NVENC y AMF (encabezados), libvpl, libopenh264, libdav1d y zlib.
- Mac: `.github/workflows/ffmpeg-mac.yml`. Tarball oficial, VideoToolbox y AudioToolbox, sin bibliotecas externas.

Los workflows se incluyen en `workflows/` de este repositorio para que se puedan leer sin acceso al repositorio privado.

## Cómo reemplazar el FFmpeg de la aplicación

La LGPL permite usar otra versión compatible de FFmpeg con Goal Labs. Los binarios viven en la carpeta `resources/ffmpeg/` de la instalación (en Windows, dentro de la carpeta de Goal Labs en Archivos de programa). Se pueden reemplazar `ffmpeg.exe`, `ffprobe.exe` y las DLL por otro build de la misma versión mayor que tenga los mismos codificadores; la aplicación verifica que existan al arrancar.

## Licencias

- FFmpeg: LGPL 2.1 o posterior. Texto en `LICENSE.txt` de cada zip y en `COPYING.LGPLv2.1` del código fuente.
- Bibliotecas externas: ver `SOURCES.md` dentro de cada zip. Las de ejecución de MinGW (libgcc, libstdc++, libwinpthread) van con la excepción de la biblioteca de ejecución de GCC, que permite distribuirlas con programas de cualquier licencia.
- Este repositorio no contiene código de Goal Labs. La aplicación tiene su propia licencia.

Consultas: soporte@goallabs.com.ar
