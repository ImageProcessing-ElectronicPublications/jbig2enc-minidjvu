# jbig2enc-minidjvu

Using [jbig2enc](https://github.com/agl/jbig2enc) in conjunction with [minidjvu](https://github.com/barak/minidjvu)/[minidjvu-mod](https://github.com/trufanov-nok/minidjvu-mod).

The [jbig2enc](https://github.com/agl/jbig2enc) implementation uses the [leptonica](https://github.com/DanBloomberg/leptonica) classifier for lossy compression, which is unsatisfactory of:

```
Kjbig2 = Kpack / (1.0 - Kerror)

         Kpack = size_jbig2 / size_pbm
         
         Kerror = sqrt(1.0 - part_no_error * part_no_error)
         
                  part_no_error = (full - error) / full
```

To overcome poor compression performance and classification errors, a recipe will be shown for using the third-party [minidjvu-mod](https://github.com/trufanov-nok/minidjvu-mod) classifier with increasing the threshold of the [leptonica](https://github.com/DanBloomberg/leptonica) classifier to eliminate classification errors.
