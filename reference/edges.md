# Edge / Line Detection

Best results are obtained by finding edges with `image_canny()` and then
performing Hough-line detection on the edge image.

## Usage

``` r
image_edge(image, radius = 1)

image_canny(image, geometry = "0x1+10%+30%")

image_hough_draw(
  image,
  geometry = NULL,
  color = "red",
  bg = "transparent",
  size = 3,
  overlay = FALSE
)

image_hough_txt(image, geometry = NULL, format = c("mvg", "svg"))
```

## Arguments

- image:

  magick image object returned by
  [`image_read()`](https://docs.ropensci.org/magick/reference/editing.md)
  or
  [`image_graph()`](https://docs.ropensci.org/magick/reference/device.md)

- radius:

  edge size in pixels

- geometry:

  geometry string, see details.

- color:

  a valid [color string](https://imagemagick.org/Magick++/Color.html)
  such as `"navyblue"` or `"#000080"`. Use `"none"` for transparency.

- bg:

  background color

- size:

  size in points to draw the line

- overlay:

  composite the drawing atop the input image. Only for
  `bg = 'transparent'`.

- format:

  output format of the text, either `svg` or `mvg`

## Details

For Hough-line detection, the geometry format is `{W}x{H}+{threshold}`
defining the size and threshold of the filter used to find 'peaks' in
the intermediate search image. For canny edge detection the format is
`{radius}x{sigma}+{lower%}+{upper%}`. More details and examples are
available at the [imagemagick
website](https://legacy.imagemagick.org/Usage/transform/).

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
if(magick_config()$version > "6.8.9"){
shape <- demo_image("shape_rectangle.gif")
rectangle <- image_canny(shape)
rectangle |> image_hough_draw('5x5+20')
rectangle |> image_hough_txt(format = 'svg') |> cat()
}
#> <?xml version="1.0" standalone="no"?>
#> <!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 20010904//EN"
#>   "http://www.w3.org/TR/2001/REC-SVG-20010904/DTD/svg10.dtd">
#> <svg width="100" height="100">
#> <desc>Hough line transform: 5x5+20</desc>
#> <desc>x1,y1  x2,y2 # count angle distance</desc>
#>   <line x1="50.5774" y1="0" x2="-7.15768" y2="100"/>
#> <desc>22 30 46</desc>
#>   <line x1="0" y1="7.99262" x2="100" y2="63.4235"/>
#> <desc>35 119 58</desc>
#>   <line x1="0" y1="6.54068" x2="100" y2="66.6267"/>
#> <desc>35 121 59</desc>
#>   <line x1="0" y1="35.5662" x2="100" y2="93.3013"/>
#> <desc>50 120 83</desc>
#>   <line x1="108.312" y1="0" x2="50.5774" y2="100"/>
#> <desc>24 30 96</desc>
#> </svg>
```
