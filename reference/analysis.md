# Image Analysis

Functions for image calculations and analysis. This part of the package
needs more work.

## Usage

``` r
image_compare(image, reference_image, metric = "", fuzz = 0)

image_compare_dist(image, reference_image, metric = "", fuzz = 0)

image_fft(image)
```

## Arguments

- image:

  magick image object returned by
  [`image_read()`](https://docs.ropensci.org/magick/reference/editing.md)
  or
  [`image_graph()`](https://docs.ropensci.org/magick/reference/device.md)

- reference_image:

  another image to compare to

- metric:

  string with a
  [metric](https://imagemagick.org/script/command-line-options.php#metric)
  from
  [metric_types()](https://docs.ropensci.org/magick/reference/options.md)
  such as `"AE"` or `"phash"`

- fuzz:

  relative color distance (value between 0 and 100) to be considered
  similar in the filling algorithm

## Details

For details see [Image++](https://imagemagick.org/Magick++/Image++.html)
documentation. Short descriptions:

- image_compare calculates a metric by comparing image with a reference
  image.

- image_fft returns Discrete Fourier Transform (DFT) of the image as a
  magnitude / phase image pair. I wish I knew what this means.

Here `image_compare()` is vectorized over the first argument and returns
the diff image with the calculated distortion value as an attribute.

## See also

Other image:
[`_index_`](https://docs.ropensci.org/magick/reference/magick.md),
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
[`transform()`](https://docs.ropensci.org/magick/reference/transform.md),
[`video`](https://docs.ropensci.org/magick/reference/video.md)

## Examples

``` r
out1 <- image_blur(logo, 3)
out2 <- image_oilpaint(logo, 3)
input <- c(logo, out1, out2, logo)
if(magick_config()$version >= "6.8.7"){
  diff_img <- image_compare(input, logo, metric = "AE")
  attributes(diff_img)
}
#> $class
#> [1] "magick-image"
#> 
#> $distortion
#> [1]     0 50455 20580     0
#> 
```
