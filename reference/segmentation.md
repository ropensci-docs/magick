# Image Segmentation

Basic image segmentation like connected components labelling, blob
extraction and fuzzy c-means

## Usage

``` r
image_connect(image, connectivity = 4)

image_split(image, keep_color = TRUE)

image_fuzzycmeans(image, min_pixels = 1, smoothing = 1.5)
```

## Arguments

- image:

  magick image object returned by
  [`image_read()`](https://docs.ropensci.org/magick/reference/editing.md)
  or
  [`image_graph()`](https://docs.ropensci.org/magick/reference/device.md)

- connectivity:

  number neighbor colors which are considered part of a unique object

- keep_color:

  if TRUE the output images retain the color of the input pixel. If
  FALSE all matching pixels are set black to retain only the image mask.

- min_pixels:

  the minimum number of pixels contained in a hexahedra before it can be
  considered valid (expressed as a percentage)

- smoothing:

  the smoothing threshold which eliminates noise in the second
  derivative of the histogram (higher values gives smoother second
  derivative)

## Details

- image_connect Connect adjacent pixels with the same pixel intensities
  to do blob extraction

- image_split Splits the image according to pixel intensities

- image_fuzzycmeans Fuzzy c-means segmentation of the histogram of color
  components

image_connect performs blob extraction by scanning the image,
pixel-by-pixel from top-left to bottom-right where regions of adjacent
pixels which share the same set of intensity values get combined.

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
[`transform()`](https://docs.ropensci.org/magick/reference/transform.md),
[`video`](https://docs.ropensci.org/magick/reference/video.md)

## Examples

``` r
# Split an image by color
img <- image_quantize(logo, 4)
layers <- image_split(img)
layers
#> # A tibble: 4 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 PNG      640    480 sRGB       TRUE         0 72x72  
#> 2 PNG      640    480 sRGB       TRUE         0 72x72  
#> 3 PNG      640    480 sRGB       TRUE         0 72x72  
#> 4 PNG      640    480 sRGB       TRUE         0 72x72  

# This returns the original image
image_flatten(layers)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 PNG      640    480 sRGB       TRUE         0 72x72  

# From the IM website
objects <- image_convert(demo_image("objects.gif"), colorspace = "Gray")
objects
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      256    171 Gray       FALSE        0 72x72  

# \donttest{
# Split image in blobs of connected pixel levels
if(magick_config()$version > "6.9.0"){
objects |>
  image_connect(connectivity = 4) |>
  image_split()

# Fuzzy c-means
image_fuzzycmeans(logo)

logo |>
  image_convert(colorspace = "HCL") |>
  image_fuzzycmeans(smoothing = 5)
}
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 HCL        FALSE        0 72x72  
# }
```
