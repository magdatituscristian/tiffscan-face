# tiffscan-face
TIFF image scanner for Face recognition


The typical use case for this high speed Node.js module is to convert large images in common formats to smaller, web-friendly JPEG, PNG and WebP images of varying dimensions.

Resizing an image is typically 4x-5x faster than using the quickest ImageMagick and GraphicsMagick settings.

Colour spaces, embedded ICC profiles and alpha transparency channels are all handled correctly. Lanczos resampling ensures quality is not sacrificed for speed.

As well as image resizing, operations such as rotation, extraction, compositing and gamma correction are available.

Most modern 64-bit OS X, Windows and Linux systems running Node versions 6, 8, 10, 11 and 12 do not require any additional install or runtime dependencies.

Examples
const sharp = require('sharp');
Callback
sharp(inputBuffer)
  .resize(320, 240)
  .toFile('output.webp', (err, info) => { ... });
Promise
sharp('input.jpg')
  .rotate()
  .resize(200)
  .toBuffer()
  .then( data => { ... })
  .catch( err => { ... });
Async/await
const semiTransparentRedPng = await sharp({
  create: {
    width: 48,
    height: 48,
    channels: 4,
    background: { r: 255, g: 0, b: 0, alpha: 0.5 }
  }
})
  .png()
  .toBuffer();
Stream
const roundedCorners = Buffer.from(
  '<svg><rect x="0" y="0" width="200" height="200" rx="50" ry="50"/></svg>'
);

const roundedCornerResizer =
  sharp()
    .resize(200, 200)
    .composite([{
      input: roundedCorners,
      blend: 'dest-in'
    }])
    .png();

readableStream
  .pipe(roundedCornerResizer)
  .pipe(writableStream);
