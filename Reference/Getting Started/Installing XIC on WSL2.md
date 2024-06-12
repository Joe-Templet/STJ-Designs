
I am trying to build XIC from source because every time I try to use the precompiled on WSL2, something is amiss. Nowadays especially, the compiled are not up to date with 

- Ensure all dependencies for Ubuntu are installed. Follow his naming, though some packages don't exist any more
- Deactivate conda - qmake is clobbering
- I set qmake to v6 (`qtchooser install qt6 $(which qmake6)`) -> `QT_VERSION=qt6`
- Build Process
	- `sudo make config` (or `make reconfig`after first try)
	- `sudo make all`
	- `sudo make packages`
	- `./xt_base/packages/pkgfiles: sudo ../util/wr_install all`
		- P1 - Currently no XIC package builds so something is wrong
- Potential Solutions to P1
	- I tried to use qt6 for most up-to-date. DON'T change makefile to sat `--enable-qt6=yes`, keep tipped `--enable-qt5=yes`and change which qt_version qmake uses
	- If it was that I wasn't doing `sudo` I'm gonna be pissed