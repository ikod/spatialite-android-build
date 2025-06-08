# Build mod_spatialite for android

Result is native mod_spatialite with required shared libraries:
```
$ unzip -t mod_spatialite_aarch64-linux-android.zip 
Archive:  mod_spatialite_aarch64-linux-android.zip
    testing: libc++_shared.so         OK
    testing: libgeos.so               OK
    testing: libgeos_c.so             OK
    testing: liblog.so                OK
    testing: libproj.so               OK
    testing: librttopo.so             OK
    testing: mod_spatialite.so        OK
```

### configure for libspatialite
```
./configure --prefix=${BUILD}
--enable-module-only
--enable-freexl=no
--enable-minizip=no
--enable-libxml2=no
--enable-iconv=no
--enable-examples=no

--build=x86_64-unknown-linux-gnu 
--host=x86_64-android-linux

--with-geosconfig=${BUILD}/bin/geos-config \
--with-sysroot=${NDK}/toolchains/llvm/prebuilt/linux-x86_64/sysroot
--target=android
```

--build - where we build, --host - target system


### Idon't need FreeXL
```
FreeXL (http://www.gaia-gis.it/FreeXL/) 
---------------------------------------
  This is recommended if you want to be able to import data from Microsoft
  Excel format (.xls suffix) files. If you do not wish to use it, you will
  need to pass --enable-freexl=no to the ./configure script. Version 0.0.4
  or later is required.
```
### I don't need ICONV as we build on linux

```
ICONV [Windows]  
---------------
When building on Windows, then you also need to provide iconv to ensure that
appropriate character set conversions are available. This dependency is not 
usually an issue when building on Linux or Mac OS X, because these systems 
provide iconv as a standard component.
```
