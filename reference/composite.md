# Image Composite

Similar to the ImageMagick `composite` utility: compose an image on top
of another one using a
[CompositeOperator](https://imagemagick.org/Magick++/Enumerations.html#CompositeOperator).

## Usage

``` r
image_composite(
  image,
  composite_image,
  operator = "atop",
  offset = "+0+0",
  gravity = "northwest",
  compose_args = ""
)

image_border(image, color = "lightgray", geometry = "10x10", operator = "copy")

image_frame(image, color = "lightgray", geometry = "25x25+6+6")

image_shadow_mask(image, geometry = "50x10+30+30")

image_shadow(
  image,
  color = "black",
  bg = "none",
  geometry = "50x10+30+30",
  operator = "copy",
  offset = "+20+20"
)

image_shade(image, azimuth = 30, elevation = 30, color = FALSE)
```

## Arguments

- image:

  magick image object returned by
  [`image_read()`](https://docs.ropensci.org/magick/reference/editing.md)
  or
  [`image_graph()`](https://docs.ropensci.org/magick/reference/device.md)

- composite_image:

  composition image

- operator:

  string with a [composite
  operator](https://imagemagick.org/Magick++/Enumerations.html#CompositeOperator)
  from
  [compose_types()](https://docs.ropensci.org/magick/reference/options.md)

- offset:

  string with either a
  [gravity_type](https://docs.ropensci.org/magick/reference/options.md)
  or a
  [geometry_point](https://docs.ropensci.org/magick/reference/geometry.md)
  to set position of top image.

- gravity:

  string with
  [gravity](https://imagemagick.org/Magick++/Enumerations.html#GravityType)
  value from
  [gravity_types](https://docs.ropensci.org/magick/reference/options.md).

- compose_args:

  additional arguments needed for some composite operations

- color:

  Set to true to shade the red, green, and blue components of the image.

- geometry:

  a [geometry string](https://imagemagick.org/Magick++/Geometry.html) to
  set height and width of the border, e.g. `"10x8"`. In addition
  image_frame allows for adding shadow by setting an offset e.g.
  `"20x10+7+2"`.

- bg:

  background color

- azimuth:

  position of light source

- elevation:

  position of light source

## Details

The `image_composite` function is vectorized over both image arguments:
if the first image has `n` frames and the second `m` frames, the output
image will contain `n` \* `m` frames.

The image_border function creates a slightly larger solid color frame
and then composes the original frame on top. The image_frame function is
similar but has an additional feature to create a shadow effect on the
border (which is really ugly).

## See also

Other image:
[`_index_`](https://docs.ropensci.org/magick/reference/magick.md),
[`analysis`](https://docs.ropensci.org/magick/reference/analysis.md),
[`animation`](https://docs.ropensci.org/magick/reference/animation.md),
[`attributes()`](https://docs.ropensci.org/magick/reference/attributes.md),
[`color`](https://docs.ropensci.org/magick/reference/color.md),
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
# Compose images using one of many operators
imlogo <- image_scale(image_read("logo:"), "x275")
rlogo <- image_read("https://jeroen.github.io/images/Rlogo-old.png")

# Standard is atop
image_composite(imlogo, rlogo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      367    275 sRGB       FALSE        0 72x72  

# Same as 'blend 50' in the command line
image_composite(imlogo, rlogo, operator = "blend", compose_args="50")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      367    275 sRGB       FALSE        0 72x72  

# Offset can be geometry or gravity
image_composite(logo, rose, offset = "+100+100")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
image_composite(logo, rose, gravity = "East")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  

# Add a border frame around the image
image_border(imlogo, "red", "10x10")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      387    295 sRGB       FALSE        0 72x72  
image_frame(imlogo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      417    325 sRGB       FALSE        0 72x72  
image_shadow(imlogo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      417    325 sRGB       TRUE         0 72x72  
image_shade(imlogo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      367    275 sRGB       FALSE        0 72x72  
```
