# jbig2enc-minidjvu

## Recipe for using the third-party classifier [minidjvu-mod](https://github.com/trufanov-nok/minidjvu-mod) with increasing the [leptonica](https://github.com/DanBloomberg/leptonica) threshold to eliminate classification errors.

Step 1: Classification and averaging of characters in [minidjvu-mod](https://github.com/trufanov-nok/minidjvu-mod) with DjVu file generation:
```shell
minidjvu-mod -A -v -a 25 -d 600 *.tif book.djvu
```
Step 2: Decoding a DjVu file back to TIFF:

Recipe 1: Decoding to multi-page TIFF and then split:
```shell
ddjvu -format=tiff book.djvu book.tif
mkdir p
tiffsplit book.tif p/x
cd p
```
Recipe 2: Convert DjVu to one-pagers and then convert to one-page TIFFs:
```shell
mkdir p
djvmcvt -i book.djvu p index.djvu
cd p
rm -fv index.djvu
for tdjvu in *.djvu; do ddjvu -mode=mask -format=pbm $tdjvu - | pnmtotiff -g4 > ${tdjvu%.djvu}.tif; echo $tdjvu; done
```

Step 3: Set DPI for TIFF:
```shell
for ttif in *.tif; do tiffset -s 282 600.0 $ttif; tiffset -s 283 600.0 $ttif; echo $ttif; done
```

Step 4: Dividing TIFF into notebooks (directories) of 10 pages:
```shell
i=0; c=10; for f in *.tif; do d=$(printf %04d $((i/$c+1))); mkdir -pv $d; mv "$f" $d; let i++; done
```

Step 5: Encoding notebooks (directories) of 10 pages each with a high classifier threshold, which is why only characters averaged in `minidjvu-mod` are classified:
```shell
mkdir -pv out; for td in 0???; do cd $td; jbig2 -s -a -p -t 0.95 -v *.tif && jbig2topdf.py output > ../out/out-$td.pdf; cd -; done
```
Step 6: Combine the 10-page notebooks:
```shell
cd out
pdfunite *.pdf book.pdf
```

As a result, you get a book that is optimal in all respects: adjustability and adequacy of the classifier (`minidjvu-mod -a "value"`), degree of filtering/compression, display time in the viewer (very fast due to 10-page notebooks).

PS: Since all the listed commands are listed in favorites [hh](https://github.com/dvorka/hstr), there are no problems at all with typing them.

