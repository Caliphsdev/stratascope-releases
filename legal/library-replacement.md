# Replacing LGPL libraries

Installed releases use folder-based packaging and dynamically loaded Qt libraries. In a Velopack
installation, the running application is in `%LOCALAPPDATA%/StrataScope.Desktop/current`.
PySide6 libraries are normally under `_internal/PySide6`; other native dependencies are listed in
the release component inventory. Do not change the separate Update.exe launcher to replace Qt.

1. Close StrataScope and all its workers. Back up the application folder and your projects.
2. Obtain the corresponding source archives delivered with that release. Build the replacement
   library with the same architecture, Qt/PySide ABI, compiler runtime and required features.
3. Replace the relevant DLLs and Python extension modules together where their ABIs require it.
   Keep filenames and dependent libraries consistent with the original package.
4. Start the application and test the functions using that library. Restore your backup if needed.

No application startup hash check rejects a library solely because you lawfully modified it.
Signed update checks apply to downloaded publisher updates, not your installed LGPL modifications.
Choose Notify only before modifying libraries: an explicitly installed publisher update replaces
the application directory, so keep your replacement build and reapply it afterward if compatible.

Release-specific source archives, build commands, patches and versions must be supplied with each
public release. Until that record is complete, the distribution gate remains closed.
