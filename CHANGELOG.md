# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog], and this project adheres to
[Semantic Versioning].

## [Unreleased]

## [0.8.2] - 2019-11-06
### Changed
* `glam_assert!` is no longer enabled by default in debug builds, it can be
  enabled in any configuration using the `glam-assert` feature or in debug
  builds only using the `debug-glam-assert` feature.
### Removed
* `glam_assert!`'s checking `lerp` is bounded between 0.0 and 1.0 and that
  matrix scales are non-zero have been removed.

## [0.8.1] - 2019-11-03
### Added
* Added `Display` trait implementations for `Mat2`, `Mat3` and `Mat4`.

### Changed
* Disabled `glam`'s SSE2 `sin_cos` implementation - it became less precise for
  large angle values.
* Reduced the default epsilon used by the `is_normalized!` macro from
  `std::f32::EPSILON` to `1e-6`.

## [0.8.0] - 2019-10-14
### Removed
* Removed the `approx` crate dependency. Each `glam` type has an `abs_diff_eq`
  method added which is used by unit tests for approximate floating point
  comparisons.
* Removed the `Angle` type. All angles are now `f32` and are expected to
  be in radians.
* Removed the deprecated `Vec2b`, `Vec3b` and `Vec4b` types and the `mask`
  methods on `Vec2Mask`, `Vec3Mask` and `Vec4Mask`.

### Changed
* The `rand` crate dependency has been removed from default features. This was
  required for benchmarking but a simple random number generator has been added
  to the benches `support` module instead.
* The `From` trait implementation converting between 1D and 2D `f32` arrays and
  matrix types have been removed. It was ambiguous how array data would map to
  matrix columns so these have been replaced with explicit methods
  `from_cols_array` and `from_cols_array_2d`.
* Matrix `new` methods have been renamed to `from_cols` to be consistent with
  the other methods that create matrices from data.
* Renamed `Mat4::perspective_glu` to `Mat4::perspective_glu_rh`.

## [0.7.2] - 2019-09-22
### Fixed
* Fixed incorrect projection matrix methods `Mat4::look_at_lh`
  and `Mat4::look_at_rh`.
### Added
* Added support for building infinite projection matrices, including both
  standard and reverse depth `Mat4::perspective_infinite_rh` and
  `Mat4::perspective_infinite_rh`.
* Added `Vec2Mask::new`, `Vec3Mask::new` and `Vec4Mask::new` methods.
* Implemented `std::ops` `BitAnd`, `BitAndAssign`, `BitOr`, `BitOrAssign`
  and `Not` traits for `Vec2Mask`, `Vec3Mask` and `Vec4Mask`.
* Added method documentation for `Vec4` and `Vec4Mask` types.
* Added missing `serde` implementations for `Mat2`, `Mat3` and `Mat4`.
* Updated `rand` and `criterion` versions.

## [0.7.1] - 2019-07-08
### Fixed
* The SSE2 implementation of `Vec4` `dot` was missing a shuffle, meaning the
  `dot`, `length`, `length_squared`, `length_reciprocal` and `normalize`
  methods were sometimes incorrect.
### Added
* Added the `glam_assert` macro which behaves like Rust's `debug_assert` but
  can be enabled separately to `debug_assert`. This is used to perform
  asserts on correctness.
* Added `is_normalized` method to `Vec2`, `Vec3` and `Vec4`.
### Changed
* Replaced usage of `std::mem::uninitialized` with `std::mem::MaybeUninit`. This
  change requires stable Rust 1.36.
* Renamed `Vec2b` to `Vec2Mask`, `Vec3b` to `Vec3Mask` and `Vec4b` to
  `Vec4Mask`. Old names are aliased to the new name and deprecated.
* Deprecate `VecNMask` `mask` method, use new `bitmask` method instead
* Made fallback version of `VecNMask` types the same size and alignment as the
  SIMD versions.
* Added `Default` support to `VecNMask` types, will add more common traits in
  the future.
* Added `#[inline]` to `mat2`, `mat3` and `mat4` functions.

## [0.7.0] - 2019-06-28
### Added
* Added `Mat2` into `[f32; 4]`, `Mat3` into `[f32; 9]` and `Mat4` into
  `[f32; 16]`.
### Changed
* Removed `impl Mul<&Vec2> for Mat2` and `impl Mul<&Vec3> for Vec3` as these
  don't exist for any other types.

## [0.6.1] - 2019-06-22
### Changed
* `Mat2` now uses a `Vec4` internally which gives it some performance
   improvements when SSE2 is available.

## 0.6.0 - 2019-06-13
### Changed
* Switched from row vectors to column vectors
  * Vectors are now on the right of multiplications with matrices and quaternions.


[Keep a Changelog]: https://keepachangelog.com/
[Semantic Versioning]: https://semver.org/spec/v2.0.0.html
[Unreleased]: https://github.com/bitshifter/glam-rs/compare/0.8.2...HEAD
[0.8.1]: https://github.com/bitshifter/glam-rs/compare/0.8.1...0.8.2
[0.8.1]: https://github.com/bitshifter/glam-rs/compare/0.8.0...0.8.1
[0.8.0]: https://github.com/bitshifter/glam-rs/compare/0.7.2...0.8.0
[0.7.2]: https://github.com/bitshifter/glam-rs/compare/0.7.1...0.7.2
[0.7.1]: https://github.com/bitshifter/glam-rs/compare/0.7.0...0.7.1
[0.7.0]: https://github.com/bitshifter/glam-rs/compare/0.6.1...0.7.0
[0.6.1]: https://github.com/bitshifter/glam-rs/compare/0.6.0...0.6.1
