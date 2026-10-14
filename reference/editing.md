# Image Editing

Read, write and join or combine images. All image functions are
vectorized, meaning they operate either on a single frame or a series of
frames (e.g. a collage, video, or animation). Besides paths and URLs,
`image_read()` supports commonly used bitmap and raster object types.

## Usage

``` r
image_read(
  path,
  density = NULL,
  depth = NULL,
  strip = FALSE,
  coalesce = TRUE,
  defines = NULL
)

image_read_svg(path, width = NULL, height = NULL)

image_read_pdf(path, pages = NULL, density = 300, password = "")

image_read_video(path, fps = 1, format = "png")

image_write(
  image,
  path = NULL,
  format = NULL,
  quality = NULL,
  depth = NULL,
  density = NULL,
  comment = NULL,
  flatten = FALSE,
  defines = NULL,
  compression = NULL
)

image_convert(
  image,
  format = NULL,
  type = NULL,
  colorspace = NULL,
  depth = NULL,
  antialias = NULL,
  matte = NULL,
  interlace = NULL,
  profile = NULL
)

image_data(image, channels = NULL, frame = 1)

image_raster(image, frame = 1, tidy = TRUE)

image_display(image, animate = TRUE)

image_browse(image, browser = getOption("browser"))

image_strip(image)

image_blank(width, height, color = "none", pseudo_image = "", defines = NULL)

image_destroy(image)

image_join(...)

image_attributes(image)

image_get_artifact(image, artifact = "")

demo_image(path)
```

## Arguments

- path:

  a file, url, or raster object or bitmap array

- density:

  resolution to render pdf or svg

- depth:

  color depth (either 8 or 16)

- strip:

  drop image comments and metadata

- coalesce:

  automatically
  [`image_coalesce()`](https://docs.ropensci.org/magick/reference/animation.md)
  gif images

- defines:

  a named character vector with extra options to control reading. These
  are the `-define key{=value}` settings in the [command line
  tool](https://imagemagick.org/script/command-line-options.php#define).
  Use an empty string for value-less defines, and NA to unset a define.

- width:

  in pixels

- height:

  in pixels

- pages:

  integer vector with page numbers. Defaults to all pages.

- password:

  user
  [password](https://docs.ropensci.org/pdftools//reference/pdf_render_page.html)
  to open protected pdf files

- fps:

  how many images to capture per second of video. Set to `NULL` to get
  all frames from the input video.

- format:

  output format such as `"png"`, `"jpeg"`, `"gif"`, `"rgb"` or `"rgba"`.

- image:

  magick image object returned by `image_read()` or
  [`image_graph()`](https://docs.ropensci.org/magick/reference/device.md)

- quality:

  number between 0 and 100 for jpeg quality. Defaults to 75.

- comment:

  text string added to the image metadata for supported formats

- flatten:

  should image be flattened before writing? This also replaces
  transparency with background color.

- compression:

  a string with compression type from
  [compress_types](https://docs.ropensci.org/magick/reference/options.md)

- type:

  string with
  [imagetype](https://imagemagick.org/Magick++/Enumerations.html#ImageType)
  value from
  [image_types](https://docs.ropensci.org/magick/reference/options.md)
  for example `grayscale` to convert into black/white

- colorspace:

  string with a
  [`colorspace`](https://imagemagick.org/Magick++/Enumerations.html#ColorspaceType)
  from
  [colorspace_types](https://docs.ropensci.org/magick/reference/options.md)
  for example `"gray"`, `"rgb"` or `"cmyk"`

- antialias:

  enable anti-aliasing for text and strokes

- matte:

  set to `TRUE` or `FALSE` to enable or disable transparency

- interlace:

  string with
  [interlace](https://imagemagick.org/Magick++/Enumerations.html#InterlaceType)

- profile:

  path to file with ICC color profile

- channels:

  string with image channel(s) for example `"rgb"`, `"rgba"`,
  `"cmyk"`,`"gray"`, or `"ycbcr"`. Default is either `"gray"`, `"rgb"`
  or `"rgba"` depending on the image

- frame:

  integer setting which frame to extract from the image

- tidy:

  converts raster data to long form for use with
  [geom_raster](https://ggplot2.tidyverse.org/reference/geom_tile.html).
  If `FALSE` output is the same as
  [`as.raster()`](https://rdrr.io/r/grDevices/as.raster.html).

- animate:

  support animations in the X11 display

- browser:

  argument passed to [browseURL](https://rdrr.io/r/utils/browseURL.html)

- color:

  a valid [color string](https://imagemagick.org/Magick++/Color.html)
  such as `"navyblue"` or `"#000080"`. Use `"none"` for transparency.

- pseudo_image:

  string with [pseudo
  image](https://imagemagick.org/script/formats.php#pseudo)
  specification for example `"radial-gradient:purple-yellow"`

- ...:

  several images or lists of images to be combined

- artifact:

  string with name of the artifact to extract, see the
  [image_deskew](https://docs.ropensci.org/magick/reference/transform.md)
  for an example.

## Details

All standard base vector methods such as
[\[](https://rdrr.io/r/base/Extract.html),
[\[\[](https://rdrr.io/r/base/Extract.html),
[`c()`](https://rdrr.io/r/base/c.html),
[`as.list()`](https://rdrr.io/r/base/list.html),
[`as.raster()`](https://rdrr.io/r/grDevices/as.raster.html),
[`rev()`](https://rdrr.io/r/base/rev.html),
[`length()`](https://rdrr.io/r/base/length.html), and
[`print()`](https://rdrr.io/r/base/print.html) can be used to work with
magick image objects. Use the standard `img[i]` syntax to extract a
subset of the frames from an image. The `img[[i]]` method is an alias
for `image_data()` which extracts a single frame as a raw bitmap matrix
with pixel values.

For reading svg or pdf it is recommended to use `image_read_svg()` and
`image_read_pdf()` if the
[rsvg](https://docs.ropensci.org/rsvg/reference/rsvg.html) and
[pdftools](https://docs.ropensci.org/pdftools//reference/pdf_render_page.html)
R packages are available. These functions provide more rendering options
(including rendering of literal svg) and better quality than built-in
svg/pdf rendering delegates from imagemagick itself.

X11 is required for `image_display()` which is only works on some
platforms. A more portable method is `image_browse()` which opens the
image in a browser. RStudio has an embedded viewer that does this
automatically which is quite nice.

Image objects are automatically released by the garbage collector when
they are no longer reachable. Because the GC only runs once in a while,
you can also call `image_destroy()` explicitly to release the memory
immediately. This is usually only needed if you create a lot of images
in a short period of time, and you might run out of memory.

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
# Download image from the web
frink <- image_read("https://jeroen.github.io/images/frink.png")
worldcup_frink <- image_fill(frink, "orange", "+100+200", 20)
image_write(worldcup_frink, "output.png")

# extract raw bitmap array
bitmap <- frink[[1]]

# replace pixels with #FF69B4 ('hot pink') and convert back to image
bitmap[,50:100, 50:100] <- as.raw(c(0xff, 0x69, 0xb4, 0xff))
image_read(bitmap)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 PNG      220    445 sRGB       TRUE         0 72x72  

# Plot to graphics device via legacy raster format
raster <- as.raster(frink)
par(ask=FALSE)
plot(raster)


# Read bitmap arrays from other image packages
download.file("https://jeroen.github.io/images/example.webp", "example.webp", mode = 'wb')
if(require(webp)) image_read(webp::read_webp("example.webp"))
#> Loading required package: webp
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 PNG      550    404 sRGB       TRUE         0 72x72  
unlink(c("example.webp", "output.png"))
if(require(rsvg)){
tiger <- image_read_svg("http://jeroen.github.io/images/tiger.svg")
svgtxt <- '<?xml version="1.0" encoding="UTF-8"?>
<svg width="400" height="400" viewBox="0 0 400 400" fill="none">
 <circle fill="steelblue" cx="200" cy="200" r="100" />
 <circle fill="yellow" cx="200" cy="200" r="90" />
</svg>'
circles <- image_read_svg(svgtxt)
}
#> Loading required package: rsvg
#> Linking to librsvg 2.58.0
if(require(pdftools))
image_read_pdf(file.path(R.home('doc'), 'NEWS.pdf'), pages = 1, density = 100)
#> Loading required package: pdftools
#> Using poppler version 24.02.0
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 PNG      850   1100 sRGB       TRUE         0 100x100
# create a solid canvas
image_blank(600, 400, "green")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 png      600    400 sRGB       FALSE        0 72x72  
image_blank(600, 400, pseudo_image = "radial-gradient:purple-yellow")
#> # A tibble: 1 × 7
#>   format          width height colorspace matte filesize density
#>   <chr>           <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 RADIAL-GRADIENT   600    400 sRGB       FALSE        0 72x72  
image_blank(200, 200, pseudo_image = "gradient:#3498db-#db3a34",
  defines = c('gradient:direction' = 'east'))
#> # A tibble: 1 × 7
#>   format   width height colorspace matte filesize density
#>   <chr>    <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GRADIENT   200    200 sRGB       FALSE        0 72x72  
```
