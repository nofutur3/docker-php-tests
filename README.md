# PHP docker image for CI

This is a docker image for testing PHP apps, it's designed to be used in CI (e.g. Bitbucket pipeline). Node with npm and yarn is included (because you may want to build assets).
Composer with prestissimo is also installed.

This image is meant to be as slim as possible. And fast. Because you don't want to waste time in your pipelines.

Works well with Symfony, Laravel and Nette. Other frameworks should work too.

**XDebug is not included**, this image is not designed for debugging PHP apps.      

## Versions (tags)

- `5.6` - deprecated, will be removed soon, security support end on 31 Dec 2018
- `7.0` - deprecated, will be removed soon, security support end on 3 Dec 2018
- `7.1`
- `7.2`
- `7.3`
- `7.4`

## Libraries

- Node v10.13.0 - LTS
- NPM
- YARN
- Composer

## Extensions


