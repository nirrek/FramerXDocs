# Framer Library Changelog

## [0.6.1] - 2018-08-16

### Added

-   onClick, onMouseDown and onMouseUp as event handlers

### Fixed

-   Setting default stack properties in package.json

## [0.6.0] - 2018-08-16

Bump version to 0.6 to avoid nmp registry conflicts in the future

### Fixed

-   Make Stack background transparent by default

## [0.2.0] - 2018-08-15

### Improved

-   Better typing of Data function

## [0.1.34] - 2018-08-15

### Added

-   Added private API for CSS exporting from a component

### Improved

-   Cleaned up CSS generation

## [0.1.33] - 2018-08-15

### Improved

-   Made a deprecated PropertyStore available again

## [0.1.32] - 2018-08-15

### Fixed

-   Bug where Animatable transactions would not work well together with ObservableObjects

## [0.1.31] - 2018-08-14

### Added

-   Support for importing Design Components in code

## [0.1.30] - 2018-08-13

### Improved

-   Change boolean control titles `enabled` and `disabled` to `enabledTitle` and `disabledTitle`

## [0.1.29] - 2018-08-13

### Property Controls

-   `unit` type for number inputs (e.g. %)
-   `step` allows numbers to be floats
-   `placeholder` for string inputs
-   `hidden` function allows controls to be hidden

## [0.1.28] - 2018-08-09

### Added

-   `Data` function to create observable object that rerenders

### Fixed

-   `animate()` function updates objects with multiple Animatable values only once per animation tick

## [0.1.27] - 2018-08-1

Initial Beta 1 release
