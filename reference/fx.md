# Image FX

Apply a custom an [fx expression](https://imagemagick.org/script/fx.php)
to the image.

## Usage

``` r
image_fx(image, expression = "p", channel = NULL)

image_fx_sequence(image, expression = "p")
```

## Arguments

- image:

  magick image object returned by
  [`image_read()`](https://docs.ropensci.org/magick/reference/editing.md)
  or
  [`image_graph()`](https://docs.ropensci.org/magick/reference/device.md)

- expression:

  string with an [fx expression](https://imagemagick.org/script/fx.php)

- channel:

  a value of
  [`channel_types()`](https://docs.ropensci.org/magick/reference/options.md)
  specifying which channel(s) to set

## Details

There are two different interfaces. The image_fx function simply applies
the same fx to each frame in the input image. The image_fx_sequence
function on the other hand treats the entire input vector as a sequence,
allowing you to apply an expression with multiple input images. See
examples.

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
# Show image_fx() expression
img <- image_convert(logo, colorspace = "Gray")
gradient_x <- image_convolve(img, kernel = "Prewitt")
gradient_y <- image_convolve(img, kernel = "Prewitt:90")
gradient <- c(image_fx(gradient_x, expression = "p^2"),
                image_fx(gradient_y, expression = "p^2"))
gradient <- image_flatten(gradient, operator = "Plus")
#gradient <- image_fx(gradient, expression = "sqrt(p)")
gradient
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 RGB        FALSE        0 72x72  

# \donttest{
image_fx(img, expression = "pow(p, 0.5)")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 Gray       FALSE        0 72x72  
image_fx(img, expression = "rand()")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 Gray       FALSE        0 72x72  
# }
# Use multiple source images
# \donttest{
input <- c(logo, image_flop(logo))
image_fx_sequence(input, "(u+v)/2")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
# }
```
