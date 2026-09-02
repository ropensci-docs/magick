# Image Frames and Animation

Operations to manipulate or combine multiple frames of an image. Details
below.

## Usage

``` r
image_animate(
  image,
  fps = 10,
  delay = NULL,
  loop = 0,
  dispose = c("background", "previous", "none"),
  optimize = FALSE
)

image_coalesce(image)

image_morph(image, frames = 8)

image_mosaic(image, operator = NULL)

image_flatten(image, operator = NULL)

image_average(image)

image_append(image, stack = FALSE)

image_apply(image, FUN, ...)

image_montage(
  image,
  geometry = NULL,
  tile = NULL,
  gravity = "Center",
  bg = "white",
  shadow = FALSE
)
```

## Arguments

- image:

  magick image object returned by
  [`image_read()`](https://docs.ropensci.org/magick/reference/editing.md)
  or
  [`image_graph()`](https://docs.ropensci.org/magick/reference/device.md)

- fps:

  frames per second. Ignored if `delay` is not `NULL`.

- delay:

  delay after each frame, in 1/100 seconds. Must be length 1, or number
  of frames. If specified, then `fps` is ignored.

- loop:

  how many times to repeat the animation. Default is infinite.

- dispose:

  a frame [disposal
  method](https://legacy.imagemagick.org/Usage/anim_basics/#dispose)
  from
  [dispose_types()](https://docs.ropensci.org/magick/reference/options.md)

- optimize:

  optimize the `gif` animation by storing only the differences between
  frames. Input images must be exactly the same size.

- frames:

  number of frames to use in output animation

- operator:

  string with a [composite
  operator](https://imagemagick.org/Magick++/Enumerations.html#CompositeOperator)
  from
  [compose_types()](https://docs.ropensci.org/magick/reference/options.md)

- stack:

  place images top-to-bottom (TRUE) or left-to-right (FALSE)

- FUN:

  a function to be called on each frame in the image

- ...:

  additional parameters for `FUN`

- geometry:

  a [geometry](https://docs.ropensci.org/magick/reference/geometry.md)
  string that defines the size the individual thumbnail images, and the
  spacing between them.

- tile:

  a [geometry](https://docs.ropensci.org/magick/reference/geometry.md)
  string for example "4x5 with limits on how the tiled images are to be
  laid out on the final result.

- gravity:

  a gravity direction, if the image is smaller than the frame, where in
  the frame is the image to be placed.

- bg:

  a background color string

- shadow:

  enable shadows between images

## Details

For details see [Magick++
STL](https://imagemagick.org/Magick++/STL.html) documentation. Short
descriptions:

- image_animate coalesces frames by playing the sequence and converting
  to `gif` format.

- image_morph expands number of frames by interpolating intermediate
  frames to blend into each other when played as an animation.

- image_mosaic inlays images to form a single coherent picture.

- image_montage creates a composite image by combining frames.

- image_flatten merges frames as layers into a single frame using a
  given operator.

- image_average averages frames into single frame.

- image_append stack images left-to-right (default) or top-to-bottom.

- image_apply applies a function to each frame

The image_apply function calls an image function to each frame and joins
results back into a single image. Because most operations are already
vectorized this is often not needed. Note that `FUN()` should return an
image. To apply other kinds of functions to image frames simply use
[lapply](https://rdrr.io/r/base/lapply.html),
[vapply](https://rdrr.io/r/base/lapply.html), etc.

## See also

Other image:
[`_index_`](https://docs.ropensci.org/magick/reference/magick.md),
[`analysis`](https://docs.ropensci.org/magick/reference/analysis.md),
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
# Combine images
logo <- image_read("https://jeroen.github.io/images/Rlogo.png")
oldlogo <- image_read("https://jeroen.github.io/images/Rlogo-old.png")

# Create morphing animation
both <- image_scale(c(oldlogo, logo), "400")
image_average(image_crop(both))
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 PNG      400    304 sRGB       TRUE         0 118x118
image_animate(image_morph(both, 10))
#> # A tibble: 12 × 7
#>    format width height colorspace matte filesize density
#>    <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#>  1 gif      400    304 sRGB       TRUE         0 118x118
#>  2 gif      400    304 sRGB       TRUE         0 118x118
#>  3 gif      400    304 sRGB       TRUE         0 118x118
#>  4 gif      400    304 sRGB       TRUE         0 118x118
#>  5 gif      400    304 sRGB       TRUE         0 118x118
#>  6 gif      400    304 sRGB       TRUE         0 118x118
#>  7 gif      400    304 sRGB       TRUE         0 118x118
#>  8 gif      400    304 sRGB       TRUE         0 118x118
#>  9 gif      400    304 sRGB       TRUE         0 118x118
#> 10 gif      400    304 sRGB       TRUE         0 118x118
#> 11 gif      400    304 sRGB       TRUE         0 118x118
#> 12 gif      400    304 sRGB       TRUE         0 72x72  

# Create thumbnails from GIF
banana <- image_read("https://jeroen.github.io/images/banana.gif")
length(banana)
#> [1] 8
image_average(banana)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      365    360 sRGB       TRUE         0 72x72  
image_flatten(banana)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      365    360 sRGB       TRUE         0 72x72  
image_append(banana)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF     2920    360 sRGB       TRUE         0 72x72  
image_append(banana, stack = TRUE)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      365   2880 sRGB       TRUE         0 72x72  

# Append images together
wizard <- image_read("wizard:")
image_append(image_scale(c(image_append(banana[c(1,3)], stack = TRUE), wizard)))
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      730    720 sRGB       TRUE         0 72x72  

image_composite(banana, image_scale(logo, "300"))
#> # A tibble: 8 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      365    360 sRGB       TRUE         0 72x72  
#> 2 GIF      365    360 sRGB       TRUE         0 72x72  
#> 3 GIF      365    360 sRGB       TRUE         0 72x72  
#> 4 GIF      365    360 sRGB       TRUE         0 72x72  
#> 5 GIF      365    360 sRGB       TRUE         0 72x72  
#> 6 GIF      365    360 sRGB       TRUE         0 72x72  
#> 7 GIF      365    360 sRGB       TRUE         0 72x72  
#> 8 GIF      365    360 sRGB       TRUE         0 72x72  

# Break down and combine frames
front <- image_scale(banana, "300")
background <- image_background(image_scale(logo, "400"), 'white')
frames <- image_apply(front, function(x){image_composite(background, x, offset = "+70+30")})
image_animate(frames, fps = 10)
#> # A tibble: 8 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 gif      400    310 sRGB       TRUE         0 72x72  
#> 2 gif      400    310 sRGB       TRUE         0 72x72  
#> 3 gif      400    310 sRGB       TRUE         0 72x72  
#> 4 gif      400    310 sRGB       TRUE         0 72x72  
#> 5 gif      400    310 sRGB       TRUE         0 72x72  
#> 6 gif      400    310 sRGB       TRUE         0 72x72  
#> 7 gif      400    310 sRGB       TRUE         0 72x72  
#> 8 gif      400    310 sRGB       TRUE         0 72x72  
# Simple 4x3 montage
input <- rep(logo, 12)
image_montage(input, geometry = 'x100+10+10', tile = '4x3', bg = 'pink', shadow = TRUE)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 ""       600    372 sRGB       FALSE        0 72x72  

# With varying frame size
input <- c(wizard, wizard, logo, logo)
image_montage(input, tile = '2x2', bg = 'pink', gravity = 'southwest')
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 ""       256    252 sRGB       FALSE        0 72x72  
```
