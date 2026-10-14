# Image thresholding

Thresholding an image can be used for simple and straightforward image
segmentation. The function `image_threshold()` allows to do black and
white thresholding whereas `image_lat()` performs local adaptive
thresholding.

## Usage

``` r
image_threshold(
  image,
  type = c("black", "white"),
  threshold = "50%",
  channel = NULL
)

image_level(
  image,
  black_point = 0,
  white_point = 100,
  mid_point = 1,
  channel = NULL
)

image_lat(image, geometry = "10x10+5%")
```

## Arguments

- image:

  magick image object returned by
  [`image_read()`](https://docs.ropensci.org/magick/reference/editing.md)
  or
  [`image_graph()`](https://docs.ropensci.org/magick/reference/device.md)

- type:

  type of thresholding, either one of lat, black or white (see details
  below)

- threshold:

  pixel intensity threshold percentage for black or white thresholding

- channel:

  a value of
  [`channel_types()`](https://docs.ropensci.org/magick/reference/options.md)
  specifying which channel(s) to set

- black_point:

  value between 0 and 100, the darkest color in the image

- white_point:

  value between 0 and 100, the lightest color in the image

- mid_point:

  value between 0 and 10 used for gamma correction

- geometry:

  pixel window plus offset for LAT algorithm

## Details

- `image_threshold(type = "black")`: Forces all pixels below the
  threshold into black while leaving all pixels at or above the
  threshold unchanged

- `image_threshold(type = "white")`: Forces all pixels above the
  threshold into white while leaving all pixels at or below the
  threshold unchanged

- `image_lat()`: Local Adaptive Thresholding. Looks in a box (width x
  height) around the pixel neighborhood if the pixel value is bigger
  than the average minus an offset.

## Examples

``` r
test <- image_convert(logo, colorspace = "Gray")
image_threshold(test, type = "black", threshold = "50%")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 Gray       FALSE        0 72x72  
image_threshold(test, type = "white", threshold = "50%")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 Gray       FALSE        0 72x72  

# Turn image into BW
test |>
  image_threshold(type = "white", threshold = "50%") |>
  image_threshold(type = "black", threshold = "50%")
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 Gray       FALSE        0 72x72  

# adaptive thresholding
image_lat(test, geometry = '10x10+5%')
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 GIF      640    480 Gray       FALSE        0 72x72  
```
