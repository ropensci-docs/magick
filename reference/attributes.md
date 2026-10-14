# Image Attributes

Attributes are properties of the image that might be present on some
images and might affect image manipulation methods.

## Usage

``` r
image_comment(image, comment = NULL)

image_info(image)
```

## Arguments

- image:

  magick image object returned by
  [`image_read()`](https://docs.ropensci.org/magick/reference/editing.md)
  or
  [`image_graph()`](https://docs.ropensci.org/magick/reference/device.md)

- comment:

  string to set an image comment

## Details

Each attribute can be get and set with the same function. The
`image_info()` function returns a data frame with some commonly used
attributes.

## See also

Other image:
[`_index_`](https://docs.ropensci.org/magick/reference/magick.md),
[`analysis`](https://docs.ropensci.org/magick/reference/analysis.md),
[`animation`](https://docs.ropensci.org/magick/reference/animation.md),
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
[`transform()`](https://docs.ropensci.org/magick/reference/transform.md),
[`video`](https://docs.ropensci.org/magick/reference/video.md)
