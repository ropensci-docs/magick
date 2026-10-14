# Image Painting

The `image_fill()` function performs flood-fill by painting starting
point and all neighboring pixels of approximately the same color.
Annotate prints some text on the image.

## Usage

``` r
image_fill(image, color, point = "+1+1", fuzz = 0, refcolor = NULL)

image_annotate(
  image,
  text,
  gravity = "northwest",
  location = "+0+0",
  degrees = 0,
  size = 10,
  font = "",
  style = "normal",
  weight = 400,
  kerning = 0,
  decoration = NULL,
  color = NULL,
  strokecolor = NULL,
  strokewidth = NULL,
  boxcolor = NULL
)
```

## Arguments

- image:

  magick image object returned by
  [`image_read()`](https://docs.ropensci.org/magick/reference/editing.md)
  or
  [`image_graph()`](https://docs.ropensci.org/magick/reference/device.md)

- color:

  a valid [color string](https://imagemagick.org/Magick++/Color.html)
  such as `"navyblue"` or `"#000080"`. Use `"none"` for transparency.

- point:

  a geometry_point string indicating the starting point of the
  flood-fill

- fuzz:

  relative color distance (value between 0 and 100) to be considered
  similar in the filling algorithm

- refcolor:

  if set, `fuzz` color distance will be measured against this color, not
  the color of the starting `point`. Any color (within `fuzz` color
  distance of the given `refcolor`), connected to starting point will be
  replaced with the `color`. If the pixel at the starting point does not
  itself match the given `refcolor` (according to `fuzz`) then no action
  will be taken.

- text:

  character vector of length equal to 'image' or length 1

- gravity:

  string with
  [gravity](https://imagemagick.org/Magick++/Enumerations.html#GravityType)
  value from
  [gravity_types](https://docs.ropensci.org/magick/reference/options.md).

- location:

  geometry string with location relative to `gravity`

- degrees:

  rotates text around center point

- size:

  font-size in pixels

- font:

  string with font family such as `"sans"`, `"mono"`, `"serif"`,
  `"Times"`, `"Helvetica"`, `"Trebuchet"`, `"Georgia"`, `"Palatino"` or
  `"Comic Sans"`. See
  [`magick_fonts()`](https://docs.ropensci.org/magick/reference/options.md)
  for what is available.

- style:

  value of
  [style_types](https://docs.ropensci.org/magick/reference/options.md)
  for example `"italic"`

- weight:

  thickness of the font, 400 is normal and 700 is bold, see
  [`magick_fonts()`](https://docs.ropensci.org/magick/reference/options.md).

- kerning:

  increases or decreases whitespace between letters

- decoration:

  value of
  [decoration_types](https://docs.ropensci.org/magick/reference/options.md)
  for example `"underline"`

- strokecolor:

  a [color string](https://imagemagick.org/Magick++/Color.html) adds a
  stroke (border around the text)

- strokewidth:

  set the strokewidth of the border around the text

- boxcolor:

  a [color string](https://imagemagick.org/Magick++/Color.html) for
  background color that annotation text is rendered on.

## Details

Note that more sophisticated drawing mechanisms are available via the
graphics device using
[image_draw](https://docs.ropensci.org/magick/reference/device.md).

Setting a font, weight, style only works if your imagemagick is compiled
with fontconfig support.

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
[`segmentation`](https://docs.ropensci.org/magick/reference/segmentation.md),
[`transform()`](https://docs.ropensci.org/magick/reference/transform.md),
[`video`](https://docs.ropensci.org/magick/reference/video.md)

## Examples

``` r
logo <- image_read("logo:")
logo <- image_background(logo, 'white')
image_fill(logo, "pink", point = "+450+400")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
image_fill(logo, "pink", point = "+450+400", fuzz = 25)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       FALSE        0 72x72  
# Add some text to an image
image_annotate(logo, "This is a test")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       TRUE         0 72x72  
image_annotate(logo, "CONFIDENTIAL", size = 50, color = "red", boxcolor = "pink",
 degrees = 30, location = "+100+100")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       TRUE         0 72x72  

# Setting fonts requires fontconfig support (and that you have the font)
image_annotate(logo, "The quick brown fox", font = "monospace", size = 50)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 sRGB       TRUE         0 72x72  
```
