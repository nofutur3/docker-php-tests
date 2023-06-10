# PHP docker image for CI

This is a docker image for testing PHP apps, it's designed to be used in CI (e.g. Bitbucket pipeline). Node with npm and yarn is included (because you may want to build assets).
Composer with prestissimo is also installed.

This image is meant to be as slim as possible. And fast. Because you don't want to waste time in your pipelines.

Works well with Symfony, Laravel and Nette. Other frameworks should work too.

**XDebug is not included**, this image is not designed for debugging PHP apps.      

## Versions (tags)

- `7.1` - deprecated, will be removed soon, security support end on 24 Oct 2019
- `7.2` - deprecated, will be removed soon, security support end on 1 Oct 2020
- `7.3` - deprecated, will be removed soon, security support end on 6 Dec 2021
- `7.4` - deprecated, will be removed soon, security support end on 28 Nov 2022
- `8.0`
- `8.1`
- `8.2`

## Libraries

- Node v10.13.0 - LTS
- NPM
- YARN
- Composer
- Phive

## Extensions


