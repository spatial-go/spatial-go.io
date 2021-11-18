# Change Log
## [1.0.3] - 2021-11-18
### Added
- Geobuf compression and decompression method can be used for vector data compression, compact structure data transfer faster

## [1.0.2] - 2021-10-14
### Added
- A correlation method to verify the validity of spatial geometry
- WKB transforms Str correlation methods
- Add circular geometry

### Fix
- Fix buffer analysis bug
- Fix overlay analysis bug

## [1.0.1] - 2021-08-30
### Added
- Methods for creating spatial indexes include Kd Tree, Quad Tree, Interval Tree, and Hilbert Packed R-Tree

## [1.0.0] - 2021-08-09
### Added
- Reconstruction of geometric coverage, spatial analysis, vector construction and other related methods
- No need to install GeoOS geometric calculation library, independent implementation of space calculation methods

## [0.1.4] - 2021-06-01
### Added
- Add parsing `WKBHexStr` method
- Add`MercatorDistance`,calculating distance scale factor by latitude for Mercator

## [0.1.3] - 2021-04-07
### Added
- Add hexagon grid method
- Add GeoCSV file read method

## [0.1.3] - 2021-04-07
### Added
- Add hexagon grid method
- Add GeoCSV file read method

## [0.1.2.1] - 2021-02-10
### Fix
- Fix memory leaks and null pointers


## [0.1.2] - 2021-02-08
### Added
- Add clustering method based on K-means clustering algorithm
- Add clustering method based on DBSCAN algorithm
- Add grid cutting method

## [0.1.1] - 2021-01-15
### Added
- Add geojson data analysis method
- Add wkb data analysis method
- Add geometryCollection object analysis processing

### Changed
- The wkt analysis method is placed under the geoos/encoding/wkt package
- The space calculation method is put under the geoos/planar package

## [0.1.0] - 2020-12-22
### Added
- Add geometry basic type
- Add basic spatial calculation method
- Added wkt data format analysis
- Add test cases