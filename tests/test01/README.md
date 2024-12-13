# jbig2enc-minidjvu

## Test.

Using [jbig2enc](https://github.com/agl/jbig2enc) in conjunction with [minidjvu-mod](https://github.com/trufanov-nok/minidjvu-mod).

### Test 01.

This material was discovered while trying to transcode DjVu to PDF in 2023. This material revealed a lot of errors of the leptonica classifier in the headings and highlighted inscriptions. This material became the basis for the recipe developed and documented here. Due to the fact that the source is DjVu with classification already applied, only classification errors can be tested on this material, but not the compression level.

I found material for testing the leptonica classification on the forum:

| Destination | Screen | Params |
| --- | --- | --- |
| [test01_jbig2-ccitt_group_4.pdf](./dest/test01_jbig2-ccitt_group_4.pdf) | ![Image](./images/test01_jbig2-ccitt_group_4.png) | no JBIG2 |
| [test01_jbig2-minidjvu-t_0_85.pdf](./dest/test01_jbig2-minidjvu-t_0_85.pdf) | ![Image](./images/test01_jbig2-minidjvu-t_0_85.png) | `-t 0.85` |
| [test01_jbig2-minidjvu-t_0_92.pdf](./dest/test0t_jbig2-minidjvu-t_0_92.pdf) | ![Image](./images/test01_jbig2-minidjvu-t_0_92.png) | `-t 0.92` |

```shell
ls -1s dest
```

```shell
944 test01_jbig2-ccitt_group_4.pdf
 84 test01_jbig2-minidjvu-t_0_85.pdf
 84 test01_jbig2-minidjvu-t_0_92.pdf
```
