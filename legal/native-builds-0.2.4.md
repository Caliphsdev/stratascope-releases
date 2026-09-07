# Native library sources and replacement — StrataScope 0.2.4

The release uses unmodified upstream Windows x64 wheels, copied with PyInstaller's
folder packaging. MSONICOP has not patched their library code. Wheel repair may rename
DLLs and rewrite imports; replacing just one DLL requires retaining those filenames
and compatible dependencies. The byte inventory identifies the installed files.

## Qt, PySide and Shiboken

Qt/PySide/Shiboken are version 6.11.2. The release supplies the full Qt and pyside-setup
source archives. Qt's complete source includes Qt PDF/PDFium and its third-party code.
Additional licences and attribution records are preserved in `qt-source-notices`;
the optional Mesa software OpenGL DLL has its own `Qt-Mesa-llvmpipe-LICENSE.txt`.

Use an x64 Visual Studio 2022 C++ developer environment, Windows SDK, CMake and Ninja,
with Python 3.12 x64. Follow the build requirements supplied with the same source
version; Qt PDF also needs the toolchain prerequisites described by Qt WebEngine.
From a separate empty build folder, configure the extracted Qt tree with
`configure.bat -release -shared -opensource -confirm-license -nomake examples -nomake tests -prefix C:\Qt\6.11.2-replacement`,
then run `cmake --build . --parallel` and `cmake --install .`. Build the modules used
in the installed inventory, including Qt PDF, rather than replacing a 6.11 ABI with
a different major/minor release. These are upstream build steps, not a claim that
MSONICOP reproduced the vendor wheel build byte-for-byte.

Use the included pyside-setup source with the replacement Qt installation to build
matching bindings if the change affects the binding ABI. Its setup.py and build
documentation provide the version-specific `--qtpaths` and `--standalone` options.
The upstream Windows instructions are at
https://doc.qt.io/qtforpython-6/building_from_source/windows.html and
https://doc.qt.io/qt-6/windows-building.html. Build privately in your own workspace;
do not overwrite a running StrataScope installation while compiling.

## Rasterio and Pyogrio native dependencies

Rasterio 1.5.1 and Pyogrio 0.13.0 both pin vcpkg baseline
`89dac9685f8d0ebd0a07d8b93ed51215c3a2fb2c`. The exact vcpkg tree, including port
patches and build scripts, accompanies this release, along with both tagged Python
projects' build-source archives. Their `ci/vcpkg.json` files and wheel-building
workflows record native features, overrides and wheel repair commands. They build
GDAL 3.12.4 with GEOS 3.14.1, PROJ 9.8.1, libiconv 1.18 and SpatiaLite 5.1.0.
Rasterio also includes FreeXL 2.0.0 and overrides libaec to 1.1.7#1. FreeXL and
SpatiaLite are supplied under their MPL 1.1 option; GEOS and libiconv retain LGPL
rights. The corresponding library archives and vcpkg patches are distributed.

Extract the vcpkg tree and run its bootstrap in an x64 Visual Studio environment.
From the extracted Rasterio or Pyogrio source, use the exact `ci/vcpkg.json` manifest
and triplet specified in its included workflow. Rasterio uses `x64-windows`;
Pyogrio uses `x64-windows-dynamic-release` with `ci/custom-triplets` as an overlay.
Run `vcpkg install --x-manifest-root=ci` with those triplet/overlay arguments and a
separate install root. Its ports apply the patches to the matching source versions.
In particular, libiconv's MSVC/export patches and SpatiaLite's Makefile/configuration
patches are part of the supplied vcpkg source, not omitted proprietary modifications.

For a modified library, change the relevant port/source in your build tree, rebuild
that library and any ABI-dependent libraries, then build and repair the matching
Python wheel using the commands in its archived workflow. `delvewheel repair` embeds
the native dependencies; preserve or consistently update the repaired DLL imports
and names when replacing a package's entire `.libs` folder and extension modules.
Do not substitute the Rasterio and Pyogrio `.libs` directories for each other.

## Shapely and other components

Shapely 2.1.2's tagged build-source archive and GEOS 3.13.1 source archive accompany
the release. Its wheel build scripts record the GEOS build and wheel-repair process.
Rebuild against GEOS 3.13.1 (including your changes), then replace matching extensions
and `Shapely.libs` together if needed. The LGPL text is included.

Certifi 2026.7.22's source archive supplies its MPL-covered certificate data. Other
native components retain their bundled BSD, MIT, Apache, zlib, public-domain or
runtime-exception notices. Microsoft runtime DLLs remain Microsoft's redistributable
components; the application licence does not grant ownership of them. Do not apply
MSONICOP's redistribution restrictions to separately licensed libraries.

After closing StrataScope, back up the application folder, replace the compatible
libraries, then start the application and test PDF, raster/vector and processing
functions. No installed-library hash gate forbids lawful modifications. Publisher
updates replace the application directory: use Notify only and retain your build
so you can deliberately reapply it. See `library-replacement.md` for recovery steps.
