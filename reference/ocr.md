# Image Text OCR

Extract text from an image using the
[tesseract](https://docs.ropensci.org/tesseract/reference/tesseract.html)
package.

## Usage

``` r
image_ocr(image, language = "eng", HOCR = FALSE, ...)

image_ocr_data(image, language = "eng", ...)
```

## Arguments

- image:

  magick image object returned by
  [`image_read()`](https://docs.ropensci.org/magick/reference/editing.md)
  or
  [`image_graph()`](https://docs.ropensci.org/magick/reference/device.md)

- language:

  passed to
  [tesseract](https://docs.ropensci.org/tesseract/reference/tesseract.html).
  To install additional languages see instructions in
  [tesseract_download()](https://docs.ropensci.org/tesseract/reference/tessdata.html).

- HOCR:

  if `TRUE` return results as HOCR xml instead of plain text

- ...:

  additional parameters passed to
  [tesseract](https://docs.ropensci.org/tesseract/reference/tesseract.html)

## Details

To use this function you need to tesseract first:

      install.packages("tesseract")

Best results are obtained if you set the correct language in
[tesseract](https://docs.ropensci.org/tesseract/reference/tesseract.html).
To install additional languages see instructions in
[tesseract_download()](https://docs.ropensci.org/tesseract/reference/tessdata.html).

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
[`options()`](https://docs.ropensci.org/magick/reference/options.md),
[`painting`](https://docs.ropensci.org/magick/reference/painting.md),
[`segmentation`](https://docs.ropensci.org/magick/reference/segmentation.md),
[`transform()`](https://docs.ropensci.org/magick/reference/transform.md),
[`video`](https://docs.ropensci.org/magick/reference/video.md)

## Examples

``` r
# \donttest{
if(require("tesseract")){
img <- image_read("http://jeroen.github.io/images/testocr.png")
image_ocr(img)
image_ocr_data(img)
}
#> Loading required package: tesseract
#> # A tibble: 60 × 3
#>    word  confidence bbox          
#>    <chr>      <dbl> <chr>         
#>  1 This        96.8 36,92,96,116  
#>  2 is          96.9 109,92,129,116
#>  3 a           95.0 141,98,156,116
#>  4 lot         95.0 169,92,201,116
#>  5 of          96.4 212,92,240,116
#>  6 12          96.4 251,92,282,116
#>  7 point       96.3 296,92,364,122
#>  8 text        96.2 374,93,427,116
#>  9 to          97.0 437,93,463,116
#> 10 test        97.0 474,93,526,116
#> # ℹ 50 more rows
# }
```
