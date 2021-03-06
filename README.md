
flat-projection
==============================================================================

[![Build Status](https://travis-ci.org/Turbo87/flat-projection-rs.svg?branch=master)](https://travis-ci.org/Turbo87/flat-projection-rs)

Fast geodesic distance approximations via flat surface projection

The `FlatProjection` struct can by used to project geographical
coordinates from [WGS84] into a cartesian coordinate system.
In the projected form approximated distance and bearing calculations
can be performed much faster than on a sphere. The precision of these
calculations is very precise for distances up to about 500 km.

[WGS84]: https://en.wikipedia.org/wiki/World_Geodetic_System


Usage
------------------------------------------------------------------------------

```rust
extern crate flat_projection;

use flat_projection::FlatProjection;

fn main() {
    let (lon1, lat1) = (6.186389, 50.823194);
    let (lon2, lat2) = (6.953333, 51.301389);

    let proj = FlatProjection::new(51.05);

    let p1 = proj.project(lon1, lat1);
    let p2 = proj.project(lon2, lat2);

    let distance = p1.distance(&p2);
    // -> 75.648 km
}
```


Benchmark
------------------------------------------------------------------------------

```
$ cargo bench

flat                    time:   [329.01 ps 331.10 ps 333.29 ps]
haversine               time:   [12.244 ns 12.338 ns 12.437 ns]
vincenty                time:   [262.92 ns 266.14 ns 270.01 ns]
```

According to these results the flat surface approximation is about 37x faster
than the [Haversine] formula.

[Haversine]: https://en.wikipedia.org/wiki/Haversine_formula


Related
------------------------------------------------------------------------------

- [cheap-ruler] – Similar calculations in JavaScripts
- [cheap-ruler-cpp] – C++ port of cheap-ruler

[cheap-ruler]: https://github.com/mapbox/cheap-ruler
[cheap-ruler-cpp]: https://github.com/mapbox/cheap-ruler-cpp


License
-------------------------------------------------------------------------------

This project is released under the [MIT license](LICENSE).
