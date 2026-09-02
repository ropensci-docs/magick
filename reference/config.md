# Magick Configuration

ImageMagick can be configured to support various additional tool and
formats via external libraries. These functions show which features
ImageMagick supports on your system.

## Usage

``` r
coder_info(format)

magick_config()

magick_set_seed(seed)
```

## Arguments

- format:

  image format such as `png`, `tiff` or `pdf`.

- seed:

  integer with seed value to use

## Details

Note that `coder_info` raises an error for unsupported formats.

## References

<https://imagemagick.org/Magick++/CoderInfo.html>

## Examples

``` r
coder_info("png")
#> $name
#> [1] "PNG"
#> 
#> $description
#> [1] "Portable Network Graphics"
#> 
#> $isReadable
#> [1] "TRUE"
#> 
#> $isWritable
#> [1] "TRUE"
#> 
#> $isMultiFrame
#> [1] "FALSE"
#> 
coder_info("jpg")
#> $name
#> [1] "JPG"
#> 
#> $description
#> [1] "Joint Photographic Experts Group JFIF format"
#> 
#> $isReadable
#> [1] "TRUE"
#> 
#> $isWritable
#> [1] "TRUE"
#> 
#> $isMultiFrame
#> [1] "FALSE"
#> 
coder_info("pdf")
#> $name
#> [1] "PDF"
#> 
#> $description
#> [1] "Portable Document Format"
#> 
#> $isReadable
#> [1] "TRUE"
#> 
#> $isWritable
#> [1] "TRUE"
#> 
#> $isMultiFrame
#> [1] "TRUE"
#> 
coder_info("tiff")
#> $name
#> [1] "TIFF"
#> 
#> $description
#> [1] "Tagged Image File Format"
#> 
#> $isReadable
#> [1] "TRUE"
#> 
#> $isWritable
#> [1] "TRUE"
#> 
#> $isMultiFrame
#> [1] "TRUE"
#> 
coder_info("gif")
#> $name
#> [1] "GIF"
#> 
#> $description
#> [1] "CompuServe graphics interchange format"
#> 
#> $isReadable
#> [1] "TRUE"
#> 
#> $isWritable
#> [1] "TRUE"
#> 
#> $isMultiFrame
#> [1] "TRUE"
#> 
# Reproduce random image
magick_set_seed(123)
image_blank(200,200, pseudo_image = "plasma:fractal")
#> # A tibble: 1 × 7
#>   format   width height colorspace matte filesize density
#>   <chr>    <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GRADIENT   200    200 sRGB       FALSE        0 72x72  
```
