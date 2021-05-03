# pkg-fetch

## Changes

This fork contains [Valetudo](https://github.com/Hypfer/Valetudo)-specific changes to the upstream `pkg-fetch`

While there was hope that there would be no fork required anymore, it sadly wasn't the case due to ideological differences.

Be advised that this fork is also heavily opinionated and only caters to the use-case of Valetudo

### Armv7 Support

The upstream project [has made it abundantly clear](https://github.com/vercel/pkg-fetch/issues/109#issuecomment-831393241)
that 32 bit operating systems should die asap.

While that certainly isn't wrong, there are still many existing armv7 devices that are only 32-bit capable
with no reason to scrap them other than ideology

Think of the planet 🌍

This repo therefore contains very minimal changes to the codebase and build process, which enable the generation of
`armv7` pkg base binaries

### No ICU

Since space is limited in embedded devices, this fork is built with `'--without-intl'`

### Relative Payload Offsets

To be able to utilize UPX compression, this fork uses offsets relative to the EOF to read prelude and payload.

Be advised that this might break if you sign your binary or append anything else apart from prelude and payload to the
binary. Maybe there will be a better solution in the future. For now this shall suffice.

### Static-linking only

Since the whole point of using `pkg` is to have a binary that runs everywhere, we're doing static linking only.

### Linux-only

Unless some Windows armv7 embedded machine magically appears somewhere, this will be linux-only.

## How to Use

Fortunately, you can vendor your own pkg nodejs base binaries by using the `PKG_CACHE_PATH` environment variable to point
to a directory that is part of your codebase. e.g. `cross-env PKG_CACHE_PATH=./build_dependencies/pkg pkg --targets node16-linuxstatic-arm64 .`
