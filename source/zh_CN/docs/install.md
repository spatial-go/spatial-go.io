The project depends on [geos](https://github.com/libgeos/geos) (GEOS is a C++ port of the ​JTS Topology Suite), you need to complete the installation of `geos` first. The installation of `geos`:

1. Mac OS X(via brew)
```sh
$ brew install geos
```
2. Ubuntu or Debian
```sh
$ apt-get install libgeos-dev
```
3. Build from source code
```sh
$ wget http://download.osgeo.org/geos/geos-3.9.0.tar.bz2
$ tar xvfj geos-3.9.0.tar.bz2
$ cd geos-3.9.0
$ ./configure
$ make
$ sudo make install
```