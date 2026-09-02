# Morphology

Apply a morphology method. This is a very flexible function which can be
used to apply any morphology method with custom parameters. See
[imagemagick website](https://legacy.imagemagick.org/Usage/morphology/)
for examples.

## Usage

``` r
image_morphology(
  image,
  method = "convolve",
  kernel = "Gaussian",
  iterations = 1,
  opts = list()
)

image_convolve(
  image,
  kernel = "Gaussian",
  iterations = 1,
  scaling = NULL,
  bias = NULL
)
```

## Arguments

- image:

  magick image object returned by
  [`image_read()`](https://docs.ropensci.org/magick/reference/editing.md)
  or
  [`image_graph()`](https://docs.ropensci.org/magick/reference/device.md)

- method:

  a string with a valid method from
  [`morphology_types()`](https://docs.ropensci.org/magick/reference/options.md)

- kernel:

  either a square matrix or a string. The string can either be a
  parameterized
  [kerneltype](https://docs.ropensci.org/magick/reference/options.md)
  such as: `"DoG:0,0,2"` or `"Diamond"` or it can contain a custom
  matrix (see examples)

- iterations:

  number of iterations

- opts:

  a named list or character vector with custom attributes

- scaling:

  string with kernel scaling. The special flag `"!"` automatically
  scales to full dynamic range, for example: `"50%!"`

- bias:

  output bias string, for example `"50%"`

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
[`ocr`](https://docs.ropensci.org/magick/reference/ocr.md),
[`options()`](https://docs.ropensci.org/magick/reference/options.md),
[`painting`](https://docs.ropensci.org/magick/reference/painting.md),
[`segmentation`](https://docs.ropensci.org/magick/reference/segmentation.md),
[`transform()`](https://docs.ropensci.org/magick/reference/transform.md),
[`video`](https://docs.ropensci.org/magick/reference/video.md)

## Examples

``` r
#example from IM website:
if(magick_config()$version > "6.8.8"){
pixel <- image_blank(1, 1, 'white') |> image_border('black', '5x5')

# See the effect of Dilate method
pixel |> image_scale('800%')
pixel |> image_morphology('Dilate', "Diamond") |> image_scale('800%')

# These produce the same output:
pixel |> image_morphology('Dilate', "Diamond", iter = 3) |> image_scale('800%')
pixel |> image_morphology('Dilate', "Diamond:3") |> image_scale('800%')

# Plus example
pixel |> image_morphology('Dilate', "Plus", iterations = 2) |> image_scale('800%')

# Rose examples
rose |> image_morphology('ErodeI', 'Octagon', iter = 3)
rose |> image_morphology('DilateI', 'Octagon', iter = 3)
rose |> image_morphology('OpenI', 'Octagon', iter = 3)
rose |> image_morphology('CloseI', 'Octagon', iter = 3)

# Edge detection
man <- demo_image('man.gif')
man |> image_morphology('EdgeIn', 'Octagon')
man |> image_morphology('EdgeOut', 'Octagon')
man |> image_morphology('Edge', 'Octagon')

# Octagonal Convex Hull
 man |>
   image_morphology('Close', 'Diamond') |>
   image_morphology('Thicken', 'ConvexHull', iterations = 1)

# Thinning down to a Skeleton
man |> image_morphology('Thinning', 'Skeleton', iterations = 1)

# Specify custom kernel matrix usingn a string:
img <- demo_image("test_mag.gif")
i <- image_convolve(img, kernel = '4x5:
       0 -1  0  0
      -1 +1 -1  0
      -1 +1 -1  0
      -1 +1 +1 -1
       0 -1 -1  0 ', bias = "50%")
}
```
