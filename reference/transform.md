# Image Transform

Basic transformations like rotate, resize, crop and flip. The
[geometry](https://docs.ropensci.org/magick/reference/geometry.md)
syntax is used to specify sizes and areas.

## Usage

``` r
image_trim(image, fuzz = 0)

image_chop(image, geometry)

image_rotate(image, degrees)

image_resize(image, geometry = NULL, filter = NULL)

image_scale(image, geometry = NULL)

image_sample(image, geometry = NULL)

image_crop(image, geometry = NULL, gravity = NULL, repage = TRUE)

image_extent(image, geometry, gravity = "center", color = "none")

image_flip(image)

image_flop(image)

image_deskew(image, threshold = 40)

image_deskew_angle(image, threshold = 40)

image_page(image, pagesize = NULL, density = NULL)

image_repage(image)

image_orient(image, orientation = NULL)

image_shear(image, geometry = "10x10", color = "none")

image_distort(image, distortion = "perspective", coordinates, bestfit = FALSE)
```

## Arguments

- image:

  magick image object returned by
  [`image_read()`](https://docs.ropensci.org/magick/reference/editing.md)
  or
  [`image_graph()`](https://docs.ropensci.org/magick/reference/device.md)

- fuzz:

  relative color distance (value between 0 and 100) to be considered
  similar in the filling algorithm

- geometry:

  a [geometry](https://docs.ropensci.org/magick/reference/geometry.md)
  string specifying area (for cropping) or size (for resizing).

- degrees:

  value between 0 and 360 for how many degrees to rotate

- filter:

  string with
  [filter](https://imagemagick.org/Magick++/Enumerations.html#FilterTypes)
  type from:
  [filter_types](https://docs.ropensci.org/magick/reference/options.md)

- gravity:

  string with
  [gravity](https://imagemagick.org/Magick++/Enumerations.html#GravityType)
  value from
  [gravity_types](https://docs.ropensci.org/magick/reference/options.md).

- repage:

  resize the canvas to the cropped area

- color:

  a valid [color string](https://imagemagick.org/Magick++/Color.html)
  such as `"navyblue"` or `"#000080"`. Use `"none"` for transparency.

- threshold:

  straightens an image. A threshold of 40 works for most images.

- pagesize:

  geometry string with preferred size and location of an image canvas

- density:

  geometry string with vertical and horizontal resolution in pixels of
  the image. Specifies an image density when decoding a Postscript or
  PDF.

- orientation:

  string to set image orientation one of the
  [orientation_types](https://docs.ropensci.org/magick/reference/options.md).
  If `NULL` it applies auto-orientation which tries to infer the correct
  orientation from the Exif data.

- distortion:

  string to set image orientation one of the
  [distort_types](https://docs.ropensci.org/magick/reference/options.md).

- coordinates:

  numeric vector (typically of length 12) with distortion coordinates

- bestfit:

  if set to `TRUE` the size of the output image can be different from
  input

## Details

For details see [Magick++
STL](https://imagemagick.org/Magick++/STL.html) documentation. Short
descriptions:

- image_trim removes edges that are the background color from the image.

- image_chop removes vertical or horizontal subregion of image.

- image_crop cuts out a subregion of original image

- image_rotate rotates and increases size of canvas to fit rotated
  image.

- image_deskew auto rotate to correct skewed images

- image_resize resizes using custom
  [filterType](https://imagemagick.org/Magick++/Enumerations.html#FilterTypes)

- image_scale and image_sample resize using simple ratio and pixel
  sampling algorithm.

- image_flip and image_flop invert image vertically and horizontally

The most powerful resize function is image_resize which allows for
setting a custom resize filter. Output of image_scale is similar to
`image_resize(img, filter = "point")`.

For resize operations it holds that if no `geometry` is specified, all
frames are rescaled to match the top frame.

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
[`video`](https://docs.ropensci.org/magick/reference/video.md)

## Examples

``` r
logo <- image_read("logo:")
logo <- image_scale(logo, "400")
image_trim(logo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      287    296 sRGB       FALSE        0 72x72  
image_chop(logo, "100x20")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      300    280 sRGB       FALSE        0 72x72  
image_rotate(logo, 45)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      496    496 sRGB       FALSE        0 72x72  
# Small image
rose <- image_convert(image_read("rose:"), "png")

# Resize to 400 width or height:
image_resize(rose, "400x")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 PNG      400    263 sRGB       FALSE        0 72x72  
image_resize(rose, "x400")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 PNG      609    400 sRGB       FALSE        0 72x72  

# Resize keeping ratio
image_resize(rose, "400x400")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 PNG      400    263 sRGB       FALSE        0 72x72  

# Resize, force size losing ratio
image_resize(rose, "400x400!")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 PNG      400    400 sRGB       FALSE        0 72x72  

# Different filters
image_resize(rose, "400x", filter = "Triangle")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 PNG      400    263 sRGB       FALSE        0 72x72  
image_resize(rose, "400x", filter = "Point")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 PNG      400    263 sRGB       FALSE        0 72x72  
# simple pixel resize
image_scale(rose, "400x")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 PNG      400    263 sRGB       FALSE        0 72x72  
image_sample(rose, "400x")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 PNG      400    263 sRGB       FALSE        0 72x72  
image_crop(logo, "400x400+200+200")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      200    100 sRGB       FALSE        0 72x72  
image_extent(rose, '200x200', color = 'pink')
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 PNG      200    200 sRGB       FALSE        0 72x72  
image_flip(logo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      400    300 sRGB       FALSE        0 72x72  
image_flop(logo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      400    300 sRGB       FALSE        0 72x72  
skewed <- image_rotate(logo, 5)
deskewed <- image_deskew(skewed)
attr(deskewed, 'angle')
#> [1] -4.80068
if(magick_config()$version > "6.8.6")
  image_orient(logo)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      400    300 sRGB       FALSE        0 72x72  
image_shear(logo, "10x10")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      453    361 sRGB       FALSE        0 72x72  
building <- demo_image('building.jpg')
image_distort(building, 'perspective', c(7,40,4,30,4,124,4,123,85,122,100,123,85,2,100,30))
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 JPEG     146    150 sRGB       FALSE        0 72x72  
```
