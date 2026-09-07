# Third-party software and data

StrataScope uses Qt for Python (PySide6), Shiboken and selected Qt libraries under LGPLv3-compatible
distribution terms. These libraries remain separately replaceable. Copies of applicable LGPLv3,
GPLv3 and component licence texts accompany reviewed release packages.

The build generates a component inventory and copies available licence texts into the `licenses`
folder beside the application. The public release must also supply corresponding library source
archives and build/replacement instructions matching the shipped versions. An upstream homepage
alone is not a substitute for corresponding source delivery.

Release approval checks the actual packaged inventory, notices and source archives.
See [icon font licences](font-notices.md), [Qt source notices](qt-source-notices/README.md)
and [native library builds and patches](native-builds-0.2.4.md). The release evidence
describes the technical checks; it does not claim external legal certification.

Natural Earth country outlines: public domain, https://www.naturalearthdata.com/.
GeoNames place names: CC BY 4.0, https://www.geonames.org/. Place names and aliases were normalised
and indexed in SQLite; country attributes were reduced for the offline map.
Online basemap providers and imagery retain their individual conditions and visible attributions.
QtAwesome's bundled icon fonts retain their respective font, artwork and attribution licences.

Portions of this software are copyright © 2026 The FreeType Project
(https://www.freetype.org/). All rights reserved. FreeType is used under the FreeType
Project License option; its full FTL text and other subcomponent notices are included.
This software is based in part on the work of the Independent JPEG Group.
libffi, libkml and uriparser retain their separate MIT/BSD notices, including where
statically included in another native library. Python's TLS and geospatial TLS
libraries may use different OpenSSL versions; applicable Apache licence texts are included.

The Velopack 1.2.0 updater is distributed under the MIT licence. Copyright © 2021 Caelan Sayler
and © 2024 Velopack Ltd. The full text is included in the bundled component notices.
Source and licence: https://github.com/velopack/velopack/tree/1.2.0.

Scientific references credit equations and interpretations; they do not license unrelated paper
text or figures and do not imply endorsement by the authors, Qt, NASA, USGS or other providers.

## Native source coverage for the 0.2.4 candidate

The pinned source collection includes Qt/PySide/Shiboken 6.11.2, GEOS 3.13.1 (Shapely),
GEOS 3.14.1 (Rasterio/Pyogrio), GNU libiconv 1.18, SpatiaLite 5.1.0, FreeXL 2.0.0
and Certifi 2026.7.22. LGPL 2.1 and MPL 1.1 texts from the additional native sources
are bundled alongside the existing Qt notices. These versions were checked against
the development wheel libraries; the exact packaged inventory remains the release authority.

SpatiaLite/FreeXL source licences and Certifi's source licence apply to those components,
not to MSONICOP's application source. Matching vcpkg build recipes and patches, tagged
wheel-build sources and supplemental native notices accompany the release. Downloaded user geology and satellite
products are not redistributed as part of the application.
