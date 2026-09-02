# Set encoder defines

So called 'defines' are properties that are passed along to external
filters and libraries. Usually defines are used in
[image_read](https://docs.ropensci.org/magick/reference/editing.md) or
[image_write](https://docs.ropensci.org/magick/reference/editing.md) to
control the image encoder/decoder, but you can also set these manually
on the image object.

## Usage

``` r
image_set_defines(image, defines)
```

## Arguments

- image:

  magick image object returned by
  [`image_read()`](https://docs.ropensci.org/magick/reference/editing.md)
  or
  [`image_graph()`](https://docs.ropensci.org/magick/reference/device.md)

- defines:

  a named character vector with extra options to control reading. These
  are the `-define key{=value}` settings in the [command line
  tool](https://imagemagick.org/script/command-line-options.php#define).
  Use an empty string for value-less defines, and NA to unset a define.

## Details

The defines values must be a character string, where the names contain
the defines keys. Each name must be of the format "enc:key" where the
first part is the encoder or filter to which the key is passed. For
example `"png:...."` defines can control the encoding and decoding of
png images.

The image_set_defines function does not make a copy of the image, so the
defined values remain in the image object until they are overwritten or
unset.

## See also

Other image:
[`_index_`](https://docs.ropensci.org/magick/reference/magick.md),
[`analysis`](https://docs.ropensci.org/magick/reference/analysis.md),
[`animation`](https://docs.ropensci.org/magick/reference/animation.md),
[`attributes()`](https://docs.ropensci.org/magick/reference/attributes.md),
[`color`](https://docs.ropensci.org/magick/reference/color.md),
[`composite`](https://docs.ropensci.org/magick/reference/composite.md),
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
# Write an image
x <- image_read("https://jeroen.github.io/images/frink.png")
image_write(x, "frink.png")

# Pass some properties to PNG encoder
defines <- c("png:compression-filter" = "1", "png:compression-level" = "0")
image_set_defines(x, defines)
image_write(x, "frink-uncompressed.png")

# Unset properties
defines[1:2] = NA
image_set_defines(x, defines)
image_write(x, "frink-final.png")

# Compare size and cleanup
file.info(c("frink.png", "frink-uncompressed.png", "frink-final.png"))
#>                          size isdir mode               mtime
#> frink.png               67029 FALSE  644 2026-09-02 10:02:02
#> frink-uncompressed.png 392398 FALSE  644 2026-09-02 10:02:02
#> frink-final.png         67029 FALSE  644 2026-09-02 10:02:02
#>                                      ctime               atime uid gid uname
#> frink.png              2026-09-02 10:02:02 2026-09-02 10:02:02   0   0  root
#> frink-uncompressed.png 2026-09-02 10:02:02 2026-09-02 10:02:02   0   0  root
#> frink-final.png        2026-09-02 10:02:02 2026-09-02 10:02:02   0   0  root
#>                        grname
#> frink.png                root
#> frink-uncompressed.png   root
#> frink-final.png          root
unlink(c("frink.png", "frink-uncompressed.png", "frink-final.png"))
```
