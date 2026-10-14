# Magick Options

List option types and values supported in your version of ImageMagick.
For descriptions see [ImageMagick
Enumerations](https://imagemagick.org/Magick++/Enumerations.html).

## Usage

``` r
magick_options()

magick_fonts()

option_types()

filter_types()

metric_types()

dispose_types()

compose_types()

colorspace_types()

channel_types()

image_types()

kernel_types()

noise_types()

gravity_types()

orientation_types()

morphology_types()

style_types()

decoration_types()

compress_types()

distort_types()

virtual_pixel_methods()

dump_option_info(option = "font")
```

## Arguments

- option:

  one of the option_types

## Details

The dump_option_info function is equivalent to calling
`convert -list [option]` on the command line. It does not return
anything, it only makes ImageMagick print stuff to the console, use only
for debugging.

## References

ImageMagick Manual:
[Enumerations](https://imagemagick.org/Magick++/Enumerations.html)

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
[`painting`](https://docs.ropensci.org/magick/reference/painting.md),
[`segmentation`](https://docs.ropensci.org/magick/reference/segmentation.md),
[`transform()`](https://docs.ropensci.org/magick/reference/transform.md),
[`video`](https://docs.ropensci.org/magick/reference/video.md)
