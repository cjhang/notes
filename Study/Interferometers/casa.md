[toc]

# Basic

`.sdm` or `.asdm`: (ALMA) Science Data Model is the general data format for the radio observation. It can be taken as an extension and full generalisation of the MeasurementSet. The small meta data is stored in XML file (one per table), and bulk data is stored in binnary format.

​	importasdm

`.ms` is the MeasurementSet (MS), including the main table and sub-table in the form of basic Unix file system. the data can be access by `browsetable` or `tb`. 



#

inp: 

1. bold parameter have subparameter, erroneous values in red



remember  to apply this primary beam correction before calculating or intensity for science.

calibration —>   flagging —>  tclean —> primary beam correction

**listobs**

- vis

```python
listobs(vis='calibrated.ms')
```

The data

- datacolumn:
  - 'data', 
  - 'corrected'
  - 'model'

`delmod` and `clearcal` can be used for delete corrected datacolumn and the model column

## Setting

change the way logger working:

```shell
casa --nologger --log2term # no GUI but message sent to terminal
casa --logfile mylogfile   # specify a logfile

casa --nologger --logfile logs/$(date +%d.%m.%y).log #put all the logs into a separate folder

# Full options
-h, --help            show this help message and exit
--logfile LOGFILE     path to log file
--log2term            direct output to terminal
--nologger            do not start CASA logger
--nologfile           do not create a log file
--nogui               avoid starting GUI tools
--rcdir RCDIR         location for startup files
--norc                do not load user config.py (startup.py is unaffected)
--colors {Neutral,NoColor,Linux,LightBG} prompt color
--pipeline            load CASA pipeline modules on startup
--agg                 startup without graphical backend
--iplog               create ipython log
--notelemetry         disable telemetry collection
--nocrashreport       do not submit an online report when CASA crashes
--datapath DATAPATH   data path(s) [colon separated]
--user-site           include user's local site-packages lib in path
(toggling this option turns it on; use startup.py to append to the path)
-c ...                python eval string or python script to execute
```



## ALMA Notes

The units of the flux density is Jy/Beam, and the Beam Area = $π(\frac{\rm FWHM}{\rm pixel})^2\frac{\ln2}{4}$.

## VLA Notes

1. Zero visibility values and shadowed data were flagged/removed (note that this already may be done by the [NRAO Data Archive](https://archive.nrao.edu/archive/advquery.jsp))
2. Reference antenna usually choose the one in the center, but not too central to suffer from the shadowing.



## Common Problems

1. Segment Fault, 

   ```shell
   ulimit -n 2048
   ```

   Some casa process will work on a large number of temporary files



## Installing package into CASA

Installing packages in CASA is fairly straightforward.  The process is described [here](http://docs.astropy.org/en/stable/install.html#installing-astropy-into-casa).  In short, you can do the following:

First, we need to make sure [pip](https://pypi.python.org/pypi/pip) is installed. Start up CASA as normal, and type:

```
CASA <1>: from setuptools.command import easy_install

CASA <2>: easy_install.main(['--user', 'pip'])

CASA <3>: import pip

CASA <4>: pip.main(['install', 'spectral-cube', '--user'])
```



Generate command line tools

```ipython
!create-symlinks
```



## Update data

To solve "Leap second table TAI_UTC seems out-of-date".

```casa
!update-data
```

Or in the terminal:

```shel
casa-config --exec update-data
```

[Reference](https://casaguides.nrao.edu/index.php/Updating_the_CASA_Data_Repository)



Run the pipeline: 

```shell
#In a Terminal
casa --pipeline
```

start casa with `casa --pipeline`

```python
# in casa
import pipeline.recipes.hifv as hifv
hifv.hifv(['mySDM'])
```


## Links

[Analysis Utilities](https://casaguides.nrao.edu/index.php?title=Analysis_Utilities)

[CASA Toolkit Reference Manual](https://casa.nrao.edu/docs/CasaRef/table-Module.html)

[MeasurementSet definition](https://casa.nrao.edu/Memos/229.html)




### CASA 6 

```python
from casatools import imager as imtool
```

| **CASA 6/casac** | **CASA 5/Class/Ctor** | **CASA 5 instance** |
| ---------------- | --------------------- | ------------------- |
| imager           | imtool                | im                  |
| calibrater       | cbtool                | cb                  |
| ms               | mstool                | ms                  |
| quanta           | qatool                | qa                  |
| table            | tbtool                | tb                  |
| agentflagger     | aftool                | af                  |
| measures         | metool                | me                  |
| image            | iatool                | ia                  |
| imagepol         | potool                | po                  |
| simulator        | smtool                | sm                  |
| componentlist    | cltool                | cl                  |
| coordsys         | cstool                | cs                  |
| regionmanager    | rgtool                | rg                  |
| spectralline     | sltool                | sl                  |
| vpmanager        | vptool                | vp                  |
| msmetadata       | msmdtool              | msmd                |
| functional       | fntool                | fn                  |
| imagemetadata    | imdtool               | imd                 |
| atmosphere       | attool                | at                  |
| calanalysis      | catool                | ca                  |
| mstransformer    | mttool                | mt                  |
| singledishms     | sdmstool              | sdms                |





## Identify the RFI:

For VLA L band https://science.nrao.edu/facilities/vla/observing/RFI/L-Band

### TFCrop

Operates on the 2D time-freq plane for each baseline and correlation. For a given baseline with certain correlation, it will first average visibility through the time to get an averaged spectrum. And then fitting the band-shape by straight line or polynomial. The RFI spikes can be detected by the sigma clip based on the fitted band-shape.

Checking how the `TFCrop` works (It is faster to check baselines separately)

```python
#>> manual testing
flagdata(vis='vis', mode='tfcrop', spw='0', datacolumn='data', action='calculate',
         antenna='ea01&ea02', display='both', ntime='scan', combinescans=False,
         timedevscale=5.0, freqdevscale=5.0, flagbackup=False)

#>> apply to the datacube
flagdata(vis=msfile, mode='tfcrop', spw='0,1', field='', antenna='',
         datacolumn='data', action='apply', display='none', 
         ntime='scan', combinescans=False,
         timedevscale=5.0, freqdevscale=5.0, flagbackup=False)
```



**notes:**

1. `ntime`: time range used for each chunk, default `ntime='scan',combinescans=False`
2. `timefit, freqfit ='line'/'poly'` set the fitted shape of the base
3. `maxnpieces ` determines the number of pieces in the polynomial fit





### RFlag

Detect outliers based on sliding-window RMS filters. It will go through for each channel (time analysis) and timestep (spectral analysis). `rflag` detects the outlier based on the baseline of the calibrated data and then mapping the flags to the original data. **It works good for low-level noisy RFI** 

Checking how the `rflag` works

```python
#>> Testing
flagdata(vis='vis', mode='rflag', spw='0', datacolumn='corrected', 
         action='calculate', antenna='ea01&ea02',
         ntime='scan', combinescans=False,
         display='both', timedevscale=5.0, freqdevscale=5.0, 
         flagbackup=False)

#>> Applying
flagdata(vis=msfile, mode='rflag', spw='0,1',field=allcal, scan='', 
         datacolumn='corrected', action='apply', display='none',
         ntime='scan', combinescans=False,
         timedevscale=5.0, freqdevscale=5.0, flagbackup=False)
```

timedevscale: threshold scaling for time deviation, the smaller means more channels will be flagged



### Extending the flags

```python
flagdata(vis=msfile, mode='extend', spw='0,1', growtime=50.0, growfreq=90.0, 
         action='apply', display='', flagbackup=False)
```



After all these flagging, it is import to have a general sense about how many data were flagged:

```python
flagInfo = flagdata(vis=msfile, mode='summary', action='calculate', display='none', spwchan=False)
```

Set the `spwchan=True` it will give the flagged fraction of every channel but will also take longer time. Set `display='report'` will plot the flag fraction of each channel if spwchann has been set and the flag fraction of each antenna.



**Third party tools**

1. [aoflagger](https://sourceforge.net/projects/aoflagger/) from LOFAR





## Reference:

For VLA beginner: [IRC+10216 Tutorial](https://casaguides.nrao.edu/index.php/Karl_G._Jansky_VLA_Tutorials#High_frequency_.2836GHz.29.2C_spectral_line_data_reduction:_Carbon_Star_IRC.2B10216) (CASA 5.5.0)

For ALMA beginner: 

RFI Flagging: [Topical Guide: Flagging VLA Data](http://casaguides.nrao.edu/index.php/VLA_CASA_Flagging) (CASA 5.5.0) [Known RFI](https://science.nrao.edu/facilities/vla/docs/manuals/obsguide/modes/rfi)





# Imaging Notes

## Continuum subtraction

There are basically two ways to subtract the continuum to obtain the emission lines. Subtracting continuum in the uv space and image space. Both have their own merits and drawbacks:

`uvcontsub`: subtracting the continuum from the uv space, it works better if the continuum is dominant the phase center.

- **Merits**: It also more robust for weak line image as few continuum deconvolution error will be present. There is also a performance benefit, since it will avoid repeating continuum deconvolution in each channel. 

- **Drawbacks**: 

  > interpolating visibilities between channels is only a good approximation for emission from near the phase center.   Thus, uv-plane based continuum subtraction will do an increasingly poor job for emission distributed further from the phase center.

`imcontsub`: subtracting the continuum from the image space. It is adequate if the continuum is weak.



## Emission Line Imaging 

**continuum subtraction**

For emission line observations, subtracting the continuum in the UV space

```python
uvcontsub(vis='vis', spw='', field='', fitspw='0~1:15~50', solint='int', 
          excludechans=True, want_cont=True)
```

**Re-gridding the data **(optional)

When combining data from different observing runs, sometimes it need to shift the dataset to the same velocity (Like the Doppler shift due to the motion of Earth)

```python
cvel2(vis='vis.contsub', outputvis='vis.contsub.cveled', 
     mode='velocity',nchan=10, start='-50km/s', width='5km/s',
     restfreq='36.39232GHz',outframe='LSRK', veltype='optical')
```

`cvel2` support multi-MS input than `cvel`, at the time of writing



**Statistics the noisy**

```python
statwt(vis='IRC10216.contsub', fitspw='0~1:15~50', excludechans=True, datacolumn='data')
```



**Remove the old files**

It is import to remove the old tclean files before start a new one. 

```python
rmtables(tablenames='vis.cube.ms*')
```



**tclean**

Set cell size to places ~5 pixels across a beam

weighting scheme: 

1. 'natural': inversely proportional to noise variance, best point source sensitivity, poor beam characteristics

  2. 'uniform': inversely proportional to sampling density (longer line has higher weight than natural), best resolution but poorer noise charateristics
  3. 'briggs': between natural and uniform, controlled by robust: -2(~ uniform), 2(~ natural), usually robust=0

continuum image

```python
imagename = ''
os.system('rm -rf {}.cont.*'.format(splitmsfile))
tclean(vis = 'calibrated.ms',
       imagename = imagename+'.cont',
       field='4~22', # field of science target
       spw='0~4',
       specmode='mfs',
       gridder='standard',
       deconvolver='hogbom',
       imsize=[400,200],
       cell='1arcsec', # places ~5 pixels across a beam
       weighting='briggs', 
       robust=0.5,
       threshold='0mJy',
       niter=50,
       interactive=True)
```



emission line 

```python
imagename = ''
os.system('rm -rf {}.*'.format(imagename))
tclean(vis = 'calibrated.ms.contsub',
       imagename = imagename,
       field = '4~22',
       spw = '0',
       specmode = 'cube',
       nchan = 70,
       restfreq = '115.271GHz' #CO(1-0)
       start = '200km/s',
       width = '10km/s',
       imsize = [500, 300],
       cell = '1arcsec',
       phasecenter = 0,
       weighting = 'briggs',
       robust = 0.5,
       interactive = True,
       niter=5000)
```

```python
tclean(vis='vis.contsub',spw='0:7~58',imagename='IRC10216_HC3N.cube',
       imsize=300,cell=['0.4arcsec'],specmode='cube',outframe='LSRK',restfreq='115.271GHz',
       perchanweightdensity=True,pblimit=-0.0001,weighting='briggs',robust=0,
       niter=100000,threshold='3.0mJy',interactive=True,savemodel='modelcolumn')
```



## Auto-Multithresh

Main  Parameter:

1. `sidelobeThreshold=3.0`
2. `noiseThreshold=5.0`
3. `lowNoiseThreshold=1.5`
4. `negativeThreshold=0.0`: it is used for absorption mask. Different from emission, absorption mask is not pruned and won't be cascaded down to low SNR data.
5. `minBeamFrac`

Second Parameter:

1. `fastNoise=True`
2. `minPercentChange=-1` : set to 1-2% can speed up the masking process
3. `doGrowPrune=True`
4. `growIteration=75` : number of iteration of binary dilation
5. `cutThreshold=0.01`

For each minor cycle (deconvolution cycle), the final mask is the combination of 'initial mask', 'grow mask' and the 'absorption mask'



## Data weighting

Natural weighting: $w_i = \frac{1}{\sigma_i^2}$

Aims for highest signal-to-noise ratio but with the poorest angular resolution.



Uniform weighting:





## Self-Calibration

Before applying self-calibration, previous tclean should have `savemodel='modelcolumn'` to set the initial model firstly. This first clean process shouldn't clean too deep, since all the fake noise will locked in the model. **At the end of the tclean, please confirm that the model has been saved in the origin measurement file ("Saving model column" in the log) and the model image only has the true structures.** Or, all the phase of antennas will be shifted to the reference antenna, which will lead to a point source image for the self-calibrated data.

The self-calibration is the same we do for the calibrator. Firstly we try to correct the quick phase variation. **It is also suggested to check the phase variation with channel firstly to avoid strong spike signals (mostly RFI)**.

```python
gaincal(vis=calfile, caltable='pcal_10min.gcal', spw='0:19~20', calmode='p',
        solint='10min',combine='scan', refant='refant', minsnr=3.0)
```

Before apply the caltable to data, checking the gaintable:

```python
plotms(vis='pcal_10min.gcal', xaxis='time', yaxis='phase', iteraxis='antenna', showgui=True)
```



 

Apply the calibration. When apply one `spw` data to others, the `spwmap=[[1,1]]` should be used, which means apply the `spw=1` calibration table to `spw=1` and `spw=2`. At the same time, the `interp='lineaerPD'` should be used.

```python
applycal(vis=calfile, field='', spw='0,1', interp=['linearPD',''],
         gaintable=['pcal_10min.gcal'], spwmap=[[1,1]], calwt=False)
```



### Primary beam correction

```python
impbcor(imagename='twhya_cont.image',
        pbimage='twhya_cont.pb',
        outfile='twhya_cont.pbcor.image')
```



## Data combination

For current VLA data, the calculated weight holds no meaning. So one should reset the weighting of the visibility before combining data from different configuration.

Two ways can be used to combine VLA data

- Reset the weighting by their channel width and integration time $\rm{weight}=2\Delta\nu\Delta t$. Using `initweights`

  ```python
  initweights(vis='msfile',wtmode='nyq')
  ```

- Calculate the weighting by the rms of the visibility

  ```python
  statwt(vis='msfile')
  ```

  It will rewrite the weighting to the visibility

> If there are strong sources in the visibility, the better way is the resetting the weights, as the RMS may be affected by the strong source. On the other hand, weighting based on RMS could be better.



## Sensitivity and resolution

In a general sense, you have to balance the sensitivity and the resolution you want for your science product. In the process of imaging, the following parameters may affect the sensitivity and resolution of the datacube:

`weighting` and `robust`



`restoringbeam`

It will make the all the channel share the same synthesized beam.



`perchanweightdensity`

It is designed to make the sensitivity more uniform for each channel as the weighting in uv is calculated independently for each channel (instead sum of all the channels). As a result, it will increase the influence of detailed uv-converage and make the clean beam size (about 12% in average) but boosts the sensitivity [[1](https://casa.nrao.edu/casadocs/casa-6.0/global-task-list/task_tclean/about),[2](https://help.almascience.org/index.php?/Knowledgebase/Article/View/417/0/HowdoesthenewperchanweightdensityparameterinCASAeffectmyALMAdata)].





## Tips for imaging

Usually 'bary' is used for sources where z>0.2 ('extragalactic") and 'lsrk is used for 'galactic' sources.





# Total Power notes

**Needs updates**

```python
import analysisUtils as aU
es = aU.stuffForScienceDataReduction()
```

```python
jyperk = es.getJyPerK(sd_ms+'.cal')

for ant in jyperk.keys():
for spw in jyperk[ant].keys():
scaleAutocorr(vis=sd_ms+'.cal', scale=jyperk[ant][spw]['mean'], antenna=ant, spw=spw)
```

