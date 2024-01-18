# Firefox for Flatpak development
This series of scripts build and install flatpak package created from already compiled Firefox sources. It's used for Firefox under flatpak development and debugging.

### First time usage
```
./0-build_flatpak_from_dir [mozilla binaries location, defaults to ~/m/mozilla-central/objdir-optimized/dist/bin]
./1-add-repo
./2-install-package
```
The installed flatpak is named as `org.mozilla.FirefoxUpstreamBinary`, in the application list named as `Firefox Nightly for Flatpak`.

### Subsequent usage (when mozilla sources has been rebuild)
```
./0-build_flatpak_from_dir [mozilla binaries location, defaults to ~/m/mozilla-central/objdir-optimized/dist/bin]
./3-update-package
```

### Typical usage

```
./mach build
cd [this cloned project location]
./0-build_flatpak_from_dir ~/mozilla-central/objdir/dist/bin
./3-update-package
```

### Using GDB for debugging

Since debuginfo is not stripped from upstream binaries you can use gdb for debugging. Note that you most likely need to change filesystem argument to point to the mozilla-central location. In order to use `--devel` option you also need `org.freedesktop.Sdk` flatpak runtime installed.
```
flatpak run --command=sh --filesystem=~/m/mozilla-central --devel org.mozilla.FirefoxUpstreamBinary
gdb /app/lib/firefox/firefox
```
