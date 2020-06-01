# pkg-fetch

This fork only exists so that there can be valetudo binaries with newer nodejs versions than currently available.

You should not use this. It is hackish and undocumented


Since cross-compiling is hard, it is recommended to run this on an armv7 machine.
Just take a Rpi3 and you should be fine. Compiling will take a while

To change the nodejs version, change `patchesJson` in `lib/upload.js`

```
npm install
npm run babel
npm run start
```