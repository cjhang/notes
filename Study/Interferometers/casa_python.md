```python
        # if inverse_image:
            # # tb = tbtool()
            # # tb.open(os.path.join(outdir, basename+suffix+'.fits'), nomodify=False)
            # # tb.put('map', -1.*tb.getcol('map'))
            # # tb.flush()
            # # tb.close()
            # with fits.open(os.path.join(outdir, basename+suffix+'.fits')) as hdu:
                # hdu[0].data = -1.0 * hdu[0].data
                # hdu.writeto(os.path.join(outdir ,basename+suffix+'.fits'), overwrite=True)

            # if uvtaper_scale:
                # tb = tbtool()
                # for taper in uvtaper_scale:
                    # tb.open(os.path.join(outdir, basename+suffix+'uvtaper{}.fits'.format(taper)), 
                            # nomodify=False)
                    # tb.put('map', -1.*tb.getcol('map'))
                    # tb.flush()
                    # tb.close()
```