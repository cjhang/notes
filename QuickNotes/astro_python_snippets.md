This is a collection of python snippets to handle small astrophisical tasks.



## Fits handling

Write fits file:

```python
# wite a fits file contains serveral table
hdr = fits.Header()
hdr['OBSERVER'] = 'Your name'
hdr['COMMENT'] = "Here's some comments about this FITS file."
primary_hdu = fits.PrimaryHDU(header=hdr)
data = np.diag([1,2,3,4])
image_hdu = fits.ImageHDU(data, name="image")
c1 = fits.Column(name='a', array=np.array([1, 2]), format='K') # double int
c2 = fits.Column(name='b', array=np.array([4, 5]), format='K') # doubel int
c3 = fits.Column(name='c', array=np.array([7., 8.]), format='D') # double float
bintable_hdu = fits.BinTableHDU.from_columns([c1, c2, c3], name='bintable')
hdus = fits.HDUList([primary_hdu, image_hdu, bintable_hdu])
hdus.writeto('data/multitable.fits', overwrite=True)

```



Vitualize the fits image

```python

```



```python
from IPython.display import set_matplotlib_formats
set_matplotlib_formats('png')
```

