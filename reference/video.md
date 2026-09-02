# Write Video

High quality video / gif exporter based on external packages
[gifski](https://r-rust.r-universe.dev/gifski/reference/gifski.html) and
[av](https://docs.ropensci.org/av//reference/encoding.html).

## Usage

``` r
image_write_video(image, path = NULL, framerate = 10, ...)

image_write_gif(image, path = NULL, delay = 1/10, ...)
```

## Arguments

- image:

  magick image object returned by
  [`image_read()`](https://docs.ropensci.org/magick/reference/editing.md)
  or
  [`image_graph()`](https://docs.ropensci.org/magick/reference/device.md)

- path:

  filename of the output gif or video. This is also the return value.

- framerate:

  frames per second, passed to
  [av_encode_video](https://docs.ropensci.org/av//reference/encoding.html)

- ...:

  additional parameters passed to
  [av_encode_video](https://docs.ropensci.org/av//reference/encoding.html)
  and
  [gifski](https://r-rust.r-universe.dev/gifski/reference/gifski.html).

- delay:

  duration of each frame in seconds (inverse of framerate)

## Details

This requires an image with multiple frames. The GIF exporter
accomplishes the same thing as
[image_animate](https://docs.ropensci.org/magick/reference/animation.md)
but much faster and with better quality.

## See also

Other image:
[`_index_`](https://docs.ropensci.org/magick/reference/magick.md),
[`analysis`](https://docs.ropensci.org/magick/reference/analysis.md),
[`animation`](https://docs.ropensci.org/magick/reference/animation.md),
[`attributes()`](https://docs.ropensci.org/magick/reference/attributes.md),
[`color`](https://docs.ropensci.org/magick/reference/color.md),
[`composite`](https://docs.ropensci.org/magick/reference/composite.md),
[`defines`](https://docs.ropensci.org/magick/reference/defines.md),
[`device`](https://docs.ropensci.org/magick/reference/device.md),
[`edges`](https://docs.ropensci.org/magick/reference/edges.md),
[`editing`](https://docs.ropensci.org/magick/reference/editing.md),
[`effects()`](https://docs.ropensci.org/magick/reference/effects.md),
[`fx`](https://docs.ropensci.org/magick/reference/fx.md),
[`geometry`](https://docs.ropensci.org/magick/reference/geometry.md),
[`morphology`](https://docs.ropensci.org/magick/reference/morphology.md),
[`ocr`](https://docs.ropensci.org/magick/reference/ocr.md),
[`options()`](https://docs.ropensci.org/magick/reference/options.md),
[`painting`](https://docs.ropensci.org/magick/reference/painting.md),
[`segmentation`](https://docs.ropensci.org/magick/reference/segmentation.md),
[`transform()`](https://docs.ropensci.org/magick/reference/transform.md)
