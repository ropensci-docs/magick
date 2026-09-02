# Convert to EBImage

Convert a Magick image to
[EBImage](https://bioconductor.org/packages/release/bioc/html/EBImage.html)
class. Note that EBImage only supports multi-frame images in greyscale.

## Usage

``` r
as_EBImage(image)
```

## Arguments

- image:

  magick image object returned by
  [`image_read()`](https://docs.ropensci.org/magick/reference/editing.md)
  or
  [`image_graph()`](https://docs.ropensci.org/magick/reference/device.md)
