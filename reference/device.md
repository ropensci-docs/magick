# Magick Graphics Device

Graphics device that produces a Magick image. Can either be used like a
regular device for making plots, or alternatively via `image_draw` to
open a device which draws onto an existing image using pixel
coordinates. The latter is vectorized, i.e. drawing operations are
applied to each frame in the image.

## Usage

``` r
image_graph(
  width = 800,
  height = 600,
  bg = "white",
  pointsize = 12,
  res = 72,
  clip = TRUE,
  antialias = TRUE
)

image_draw(image, pointsize = 12, res = 72, antialias = TRUE, ...)

image_capture()
```

## Arguments

- width:

  in pixels

- height:

  in pixels

- bg:

  background color

- pointsize:

  size of fonts

- res:

  resolution in pixels

- clip:

  enable clipping in the device. Because clipping can slow things down a
  lot, you can disable it if you don't need it.

- antialias:

  TRUE/FALSE: enables anti-aliasing for text and strokes

- image:

  an existing image on which to start drawing

- ...:

  additional device parameters passed to
  [plot.window](https://rdrr.io/r/graphics/plot.window.html) such as
  `xlim`, `ylim`, or `mar`.

## Details

The device is a relatively recent feature of the package. It should
support all operations but there might still be small inaccuracies. Also
it is a bit slower than some of the other devices, in particular for
rendering text and clipping. Hopefully this can be optimized in the next
version.

By default `image_draw` sets all margins to 0 and uses graphics
coordinates to match image size in pixels (width x height) where `(0,0)`
is the top left corner. Note that this means the y axis increases from
top to bottom which is the opposite of typical graphics coordinates. You
can override all this by passing custom `xlim`, `ylim` or `mar` values
to `image_draw`.

The `image_capture` function returns the current device as an image.
This only works if the current device is a magick device or supports
[dev.capture](https://rdrr.io/r/grDevices/dev.capture.html).

## See also

Other image:
[`_index_`](https://docs.ropensci.org/magick/reference/magick.md),
[`analysis`](https://docs.ropensci.org/magick/reference/analysis.md),
[`animation`](https://docs.ropensci.org/magick/reference/animation.md),
[`attributes()`](https://docs.ropensci.org/magick/reference/attributes.md),
[`color`](https://docs.ropensci.org/magick/reference/color.md),
[`composite`](https://docs.ropensci.org/magick/reference/composite.md),
[`defines`](https://docs.ropensci.org/magick/reference/defines.md),
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
# Regular image
frink <- image_read("https://jeroen.github.io/images/frink.png")

# Produce image using graphics device
fig <- image_graph(res = 96)
ggplot2::qplot(mpg, wt, data = mtcars, colour = cyl)
#> Warning: `qplot()` was deprecated in ggplot2 3.4.0.
dev.off()
#> agg_record_7c31191f6f9 
#>                      2 

# Combine
out <- image_composite(fig, frink, offset = "+70+30")
print(out)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 PNG      800    600 sRGB       TRUE         0 96x96  

# Or paint over an existing image
img <- image_draw(frink)
rect(20, 20, 200, 100, border = "red", lty = "dashed", lwd = 5)
abline(h = 300, col = 'blue', lwd = '10', lty = "dotted")
text(10, 250, "Hoiven-Glaven", family = "monospace", cex = 4, srt = 90)
palette(rainbow(11, end = 0.9))
symbols(rep(200, 11), seq(0, 400, 40), circles = runif(11, 5, 35),
  bg = 1:11, inches = FALSE, add = TRUE)
dev.off()
#> agg_record_7c31191f6f9 
#>                      2 
print(img)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 PNG      220    445 sRGB       TRUE         0 72x72  

# \donttest{
# Vectorized example with custom coordinates
earth <- image_read("https://jeroen.github.io/images/earth.gif")
img <- image_draw(earth, xlim = c(0,1), ylim = c(0,1))
rect(.1, .1, .9, .9, border = "red", lty = "dashed", lwd = 5)
text(.5, .9, "Our planet", cex = 3, col = "white")
dev.off()
#> agg_record_7c31191f6f9 
#>                      2 
print(img)
#> # A tibble: 44 × 7
#>    format width height colorspace matte filesize density
#>    <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#>  1 GIF      400    400 sRGB       TRUE         0 72x72  
#>  2 GIF      400    400 sRGB       TRUE         0 72x72  
#>  3 GIF      400    400 sRGB       TRUE         0 72x72  
#>  4 GIF      400    400 sRGB       TRUE         0 72x72  
#>  5 GIF      400    400 sRGB       TRUE         0 72x72  
#>  6 GIF      400    400 sRGB       TRUE         0 72x72  
#>  7 GIF      400    400 sRGB       TRUE         0 72x72  
#>  8 GIF      400    400 sRGB       TRUE         0 72x72  
#>  9 GIF      400    400 sRGB       TRUE         0 72x72  
#> 10 GIF      400    400 sRGB       TRUE         0 72x72  
#> # ℹ 34 more rows
# }
```
