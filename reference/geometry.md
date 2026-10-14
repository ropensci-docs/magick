# Geometry Helpers

ImageMagick uses a handy geometry syntax to specify coordinates and
shapes for use in image transformations. You can either specify these
manually as strings or use the helper functions below.

## Usage

``` r
geometry_point(x, y)

geometry_area(width = NULL, height = NULL, x_off = 0, y_off = 0)

geometry_size_pixels(width = NULL, height = NULL, preserve_aspect = TRUE)

geometry_size_percent(width = 100, height = NULL)
```

## Arguments

- x:

  left offset in pixels

- y:

  top offset in pixels

- width:

  in pixels

- height:

  in pixels

- x_off:

  offset in pixels on x axis

- y_off:

  offset in pixels on y axis

- preserve_aspect:

  if FALSE, resize to width and height exactly, loosing original aspect
  ratio. Only one of `percent` and `preserve_aspect` may be `TRUE`.

## Details

See [ImageMagick Manual](https://imagemagick.org/Magick++/Geometry.html)
for details about the syntax specification. Examples of `geometry`
strings:

- **`"500x300"`** – *Resize image keeping aspect ratio, such that width
  does not exceed 500 and the height does not exceed 300.*

- **`"500x300!"`** – *Resize image to 500 by 300, ignoring aspect ratio*

- **`"500x"`** – *Resize width to 500 keep aspect ratio*

- **`"x300"`** – *Resize height to 300 keep aspect ratio*

- **`"50%x20%"`** – *Resize width to 50 percent and height to 20 percent
  of original*

- **`"500x300+10+20"`** – *Crop image to 500 by 300 at position 10,20*

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
[`morphology`](https://docs.ropensci.org/magick/reference/morphology.md),
[`ocr`](https://docs.ropensci.org/magick/reference/ocr.md),
[`options()`](https://docs.ropensci.org/magick/reference/options.md),
[`painting`](https://docs.ropensci.org/magick/reference/painting.md),
[`segmentation`](https://docs.ropensci.org/magick/reference/segmentation.md),
[`transform()`](https://docs.ropensci.org/magick/reference/transform.md),
[`video`](https://docs.ropensci.org/magick/reference/video.md)

## Examples

``` r
# Specify a point
logo <- image_read("logo:")
image_annotate(logo, "Some text", location = geometry_point(100, 200), size = 24)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       TRUE         0 72x72  

# Specify image area
image_crop(logo, geometry_area(300, 300), repage = FALSE)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      300    300 sRGB       FALSE        0 72x72  
image_crop(logo, geometry_area(300, 300, 100, 100), repage = FALSE)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      300    300 sRGB       FALSE        0 72x72  

# Specify image size
image_resize(logo, geometry_size_pixels(300))
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      300    225 sRGB       FALSE        0 72x72  
image_resize(logo, geometry_size_pixels(height = 300))
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      400    300 sRGB       FALSE        0 72x72  
image_resize(logo, geometry_size_pixels(300, 300, preserve_aspect = FALSE))
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      300    300 sRGB       FALSE        0 72x72  

# resize relative to current size
image_resize(logo, geometry_size_percent(50))
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      320    240 sRGB       FALSE        0 72x72  
image_resize(logo, geometry_size_percent(50, 20))
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      320     96 sRGB       FALSE        0 72x72  
```
