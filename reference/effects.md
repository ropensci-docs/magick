# Image Effects

High level effects applied to an entire image. These are mostly just for
fun.

## Usage

``` r
image_despeckle(image, times = 1L)

image_reducenoise(image, radius = 1L)

image_noise(image, noisetype = "gaussian")

image_blur(image, radius = 1, sigma = 0.5)

image_motion_blur(image, radius = 1, sigma = 0.5, angle = 0)

image_charcoal(image, radius = 1, sigma = 0.5)

image_oilpaint(image, radius = 1)

image_emboss(image, radius = 1, sigma = 0.5)

image_implode(image, factor = 0.5)

image_negate(image)
```

## Arguments

- image:

  magick image object returned by
  [`image_read()`](https://docs.ropensci.org/magick/reference/editing.md)
  or
  [`image_graph()`](https://docs.ropensci.org/magick/reference/device.md)

- times:

  number of times to repeat the despeckle operation

- radius:

  radius, in pixels, for various transformations

- noisetype:

  string with a
  [noisetype](https://imagemagick.org/Magick++/Enumerations.html#NoiseType)
  value from
  [noise_types](https://docs.ropensci.org/magick/reference/options.md).

- sigma:

  the standard deviation of the Laplacian, in pixels.

- angle:

  angle, in degrees, for various transformations

- factor:

  image implode factor (special effect)

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
logo <- image_read("logo:")
image_despeckle(logo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
image_reducenoise(logo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
image_noise(logo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
image_blur(logo, 10, 10)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
image_motion_blur(logo, 10, 10, 45)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
image_charcoal(logo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 Gray       FALSE        0 72x72  
image_oilpaint(logo, radius = 3)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
image_emboss(logo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
image_implode(logo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
image_negate(logo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
```
