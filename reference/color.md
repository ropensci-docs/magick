# Image Color

Functions to adjust contrast, brightness, colors of the image. Details
below.

## Usage

``` r
image_modulate(image, brightness = 100, saturation = 100, hue = 100)

image_quantize(
  image,
  max = 256,
  colorspace = "rgb",
  dither = TRUE,
  treedepth = NULL
)

image_map(image, map, dither = FALSE)

image_ordered_dither(image, threshold_map)

image_channel(image, channel = "lightness")

image_separate(image, channel = "default")

image_combine(image, colorspace = "sRGB", channel = "default")

image_transparent(image, color, fuzz = 0)

image_background(image, color, flatten = TRUE)

image_virtual_pixel(image, virtual_pixel_method)

image_colorize(image, opacity, color)

image_contrast(image, sharpen = 1)

image_normalize(image)

image_enhance(image)

image_equalize(image)

image_median(image, radius = 1)
```

## Arguments

- image:

  magick image object returned by
  [`image_read()`](https://docs.ropensci.org/magick/reference/editing.md)
  or
  [`image_graph()`](https://docs.ropensci.org/magick/reference/device.md)

- brightness:

  modulation of brightness as percentage of the current value (100 for
  no change)

- saturation:

  modulation of saturation as percentage of the current value (100 for
  no change)

- hue:

  modulation of hue is an absolute rotation of -180 degrees to +180
  degrees from the current position corresponding to an argument range
  of 0 to 200 (100 for no change)

- max:

  preferred number of colors in the image. The actual number of colors
  in the image may be less than your request, but never more.

- colorspace:

  string with a
  [`colorspace`](https://imagemagick.org/Magick++/Enumerations.html#ColorspaceType)
  from
  [colorspace_types](https://docs.ropensci.org/magick/reference/options.md)
  for example `"gray"`, `"rgb"` or `"cmyk"`

- dither:

  a boolean (defaults to `TRUE`) specifying whether to apply
  Floyd/Steinberg error diffusion to the image: averages intensities of
  several neighboring pixels

- treedepth:

  depth of the quantization color classification tree. Values of 0 or 1
  allow selection of the optimal tree depth for the color reduction
  algorithm. Values between 2 and 8 may be used to manually adjust the
  tree depth.

- map:

  reference image to map colors from

- threshold_map:

  A string giving the dithering pattern to use. See [the ImageMagick
  documentation](https://legacy.imagemagick.org/Usage/quantize/#od_levels)
  for possible values

- channel:

  a string with a
  [channel](https://imagemagick.org/Magick++/Enumerations.html#ChannelType)
  from
  [channel_types](https://docs.ropensci.org/magick/reference/options.md)
  for example `"alpha"` or `"hue"` or `"cyan"`

- color:

  a valid [color string](https://imagemagick.org/Magick++/Color.html)
  such as `"navyblue"` or `"#000080"`. Use `"none"` for transparency.

- fuzz:

  relative color distance (value between 0 and 100) to be considered
  similar in the filling algorithm

- flatten:

  should image be flattened before writing? This also replaces
  transparency with background color.

- virtual_pixel_method:

  a string with a [virtual pixel
  method](https://imagemagick.org/Magick++/Enumerations.html#VirtualPixelMethod)
  from
  [virtual_pixel_methods](https://docs.ropensci.org/magick/reference/options.md).

- opacity:

  percentage of opacity used for coloring

- sharpen:

  enhance intensity differences in image

- radius:

  replace each pixel with the median color in a circular neighborhood

## Details

For details see [Magick++
STL](https://imagemagick.org/Magick++/STL.html) documentation. Short
descriptions:

- image_modulate adjusts brightness, saturation and hue of image
  relative to current.

- image_quantize reduces number of unique colors in the image.

- image_ordered_dither reduces number of unique colors using a dithering
  threshold map.

- image_map replaces colors of image with the closest color from a
  reference image.

- image_channel extracts a single channel from an image and returns as
  grayscale.

- image_transparent sets pixels approximately matching given color to
  transparent.

- image_background sets background color. When image is flattened,
  transparent pixels get background color.

- image_colorize overlays a solid color frame using specified opacity.

- image_contrast enhances intensity differences in image

- image_normalize increases contrast by normalizing the pixel values to
  span the full range of colors

- image_enhance tries to minimize noise

- image_equalize equalizes using histogram equalization

- image_median replaces each pixel with the median color in a circular
  neighborhood

- image_virtual_pixel sets the [virtual
  pixel](https://usage.imagemagick.org/misc/#virtual) filling method to
  use when a raw distortion transformation (e.g.
  [image_distort](https://docs.ropensci.org/magick/reference/transform.md))
  introduces new pixels in the image. Some high-level transformations
  (e.g.
  [image_rotate](https://docs.ropensci.org/magick/reference/transform.md)
  and
  [image_shear](https://docs.ropensci.org/magick/reference/transform.md))
  will override the virtual pixel value with a default one.

Note that colors are also determined by image properties
[imagetype](https://imagemagick.org/Magick++/Enumerations.html#ImageType)
and
[colorspace](https://imagemagick.org/Magick++/Enumerations.html#ColorspaceType)
which can be modified via
[`image_convert()`](https://docs.ropensci.org/magick/reference/editing.md).

## See also

Other image:
[`_index_`](https://docs.ropensci.org/magick/reference/magick.md),
[`analysis`](https://docs.ropensci.org/magick/reference/analysis.md),
[`animation`](https://docs.ropensci.org/magick/reference/animation.md),
[`attributes()`](https://docs.ropensci.org/magick/reference/attributes.md),
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
# manually adjust colors
logo <- image_read("logo:")
image_modulate(logo, brightness = 200)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
image_modulate(logo, saturation = 150)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
image_modulate(logo, hue = 200)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  

# Reduce image to 10 different colors using various spaces
image_quantize(logo, max = 10, colorspace = 'gray')
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 Gray       FALSE        0 72x72  
image_quantize(logo, max = 10, colorspace = 'rgb')
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 RGB        FALSE        0 72x72  
image_quantize(logo, max = 10, colorspace = 'cmyk')
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 CMYK       FALSE        0 72x72  

image_ordered_dither(logo, 'o8x8')
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
# Change background color
translogo <- image_transparent(logo, 'white')
image_background(translogo, "pink", flatten = TRUE)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       TRUE         0 72x72  

# Compare to flood-fill method:
image_fill(logo, "pink", fuzz = 20)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  

# Black virtual pixel on a 45° rotation
logo |> image_virtual_pixel("Black") |>
  image_distort("AffineProjection", sqrt(0.5) * c(1,1,-1,1,0,0), bestfit = TRUE)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      794    794 sRGB       FALSE        0 72x72  

# Tile virtual pixel on a 45° rotation
logo |> image_virtual_pixel("Tile") |>
 image_distort("AffineProjection", sqrt(0.5) * c(1,1,-1,1,0,0), bestfit = TRUE)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      794    794 sRGB       FALSE        0 72x72  

# Other color tweaks
image_colorize(logo, 50, "red")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
image_contrast(logo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
image_normalize(logo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
image_enhance(logo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
image_equalize(logo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
image_median(logo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  

# Alternate way to convert into black-white
image_convert(logo, type = 'grayscale')
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 Gray       FALSE        0 72x72  
```
