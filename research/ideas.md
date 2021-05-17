# Science Projects

## ALMACAL

ALMACAL is the ALMA ancillary project, which collects all the observations of the ALMA calibrators. 

1. Improve calibration of the calibrators

   > Possible reasons for the residual after point source subtraction:
   >
   > 1. Calibrator has been resolved. Maybe an iterative algorithm to improve the model? 
   > 2. Some remaining phase error in the calibrated visibility
   >
   > Two things can be tried:
   >
   > 1. Build one observation from scratch, find the reason for bad calibration
   > 2. Try point+gaussian model, try to capture the ears (maybe it need more parameter constrains) or more constrains on the model setup, maybe try more general tools

3. Line searching, 

   > OH$^+$ CH$^+$ are low density tracers, they are usually observed in obsorption, which can be used to search gas inflow and outflow of the blazers.  [Barte+2020]
   >
   > One thing should keep in mind is the properties of the calibrators themselves. They were blazers, no very high-accuracy redshift, and no much information about their host galaxies.

4. Magnetic field

   > Some of the calibrators should be the polorized calibrators, but the science projects may not focus on the magnetic field. Searching all the related project, and to see if there is opportinity for blind magnetic field survey.
   >
   > Maybe the magnetic filed of the calibratos themselves can be insteresting as well, like the time variation
   
6. Source finding algorithm for interferometric image map

   > Do something like inverse the imaginary, or real part to create a conterpart image, then finding source in two complementary images
   
7. ~~ALMACAL time domain data, can be used to trace the gas filaments fast motion in the early Universe?~~

   > - the residual of the central point source may dominate the noise, which will create some fake variational signal.

6. Adaption of high contrast imaging to the calibrators' imaging

   > In field of circumstellar disk or exoplanet fields, high contrast imaging technologies have been widely used, including Angular Diﬀerential Imaging (ADI, [Marois 2006](https://ui.adsabs.harvard.edu/abs/2006ApJ...641..556M/abstract))  and Diﬀerential Polarimetric Imaging (DPI, [van Holstein 2018](https://ui.adsabs.harvard.edu/abs/2020A%26A...633A..64V/abstract)).
   >
   > For ALMACAL, both of the two method can be tested
   >
   > See also [Beuzit 2019](https://ui.adsabs.harvard.edu/abs/2019A%26A...631A.155B/abstract) for more information about SPHERE

## Deep Field Science

1. Find the proto-group in deep small field observation. 

   > Galaxy group is smaller than galaxy cluster, which should be more common and more releavant for galaxy evolution in a shorter timescale

2. 

## Early Universe

1. There is initial mass function for stars, how about the initial mass function for galaxies? Will that matters for the proto-cluster formation or can it be the characteristics to distinguish different evolution stage of clusters? Any possible for the initial mass function of black whole seed at the reionization era?

   > Maybe it is a long time project. Large sample of photo-clusters is essential.

2. **Determine the kinematics of [C II] and the other gas phase tracer**

   > The [C II] has been widely used to study the kinematics or even the dynamics of high-z galaxies. However, little researchs have been focused on their validity. The FIEA on SOFIA can be the best instrument to study the [C II] kinematics of local spiral or starburst galaxies.
   >
   > **Using simalma to test the spatial resolution effect on the interpretation of the kinematics from [C II]**
   >
   > - [ ] Using data from SOFIA as the input
   > - [ ] Missing flux issue? We only see the denser structure

3. Study the role of star formation efficiency in spiral. Any enhancement?

   > This thought comes out when I read the study about the Milky Way's spiral arms. They did not find significant strengthen of SFE in the spiral arms. They argued the large star formation surface density is mainly because the higher efficiency of converting atomic hydrogen to molecular gas.
   >
   > Another crazy idea: it is possible the molecular gas are also not formed in the spiral arms, but only due to some dynamic friction+gravitational contraction?

4. Find MW analoges in the early Universe

   > SPT0418-47 galaxy is thought to be alike MK from their kinematic signature. How about the SED and the environment? (**It also has much higher SFR than MW**)

5. **Are high-z starburst galaxies are mostly regular rotation dominate?**

   > From current high resolution [C II] observations, it seems that most galaxies with strong [C II] are rotation dominated. Since most of these galaxies only barely resolved, so it needs the confirmation from higher angular observations and it would be good to have the kinematics of other gas tracers.
   >
   > One interesting simulation is to put the local detailed studied  into high redshift, to test the information we can get. Local candidates: Arp220

6. ~~Measuring the magnetic filed in the submillimeter bright galaxies and the Lyman-a galaxies in very high-z galaxies, additional evidence of the high turbulence?~~

   > The kinetic SZ effect and the synchrotron are both hard to measure at early Univere, but it definitely important for future surveys

7. Try to observe the magnetic at high-z galaxies.

   > The first ideal target could be the strong lensed source, they were bright and could reach a relative high angular resolution.
   >
   > - Red Radio Ring (Geach+2015), extremely bright (**Maybe the only one at the moment**)
   > - SPT0418-47, cold gas disk favor highly ordered magnetic field
   >
   > Two spectral window:
   >
   > 1. Far-infrared
   >
   >    - For local Universe, starburst systems have already revealed strong dust polarization
   >
   >    - For high-z lensed galaxies, it is in the higher ALMA band >B7
   >
   > 2. submilimeter
   >
   >    - For local Universe, the prototype can be M82 and NGC253
   >
   >    - For high-z lensed galaxies, it is in the ALMA lower band, <B4
   >
   > Possible plan:
   >
   > 1. NGC253, single dish submillimeter polarzation mosac observation
   > 2. z~2-3, high-z strong lensed starburst system

   

8. The rotation curve of proto-cluster: resolved central galaxies + general circular motion of the satellite galaxies

   > The best candidate for such a testing is the two hypoluminous proto-clusters find in 2018 (Oteo+2018, Miller+2018)
   >
   > One important step is to remove the peculiar motion of the galaxies, which should be intensively rely on models

9. The evolution stages of photo-cluster

   > Not only for Lyman-break and SMG, there are also proto-clusters selected from radio AGN and deep field spectral and photometrical surveys. One thing worth a try is puting all the confirmed photo-cluster together, trying to make the biggest sample to study them systematically. 
   >
   > 1. The best starting point is the HUDF, where deep ALMA, Muse, and VLA observation are both available

10. X-ray survey of SMGs

    > 1. One possible project is to make a small survey of Chandra observation for ~10 brightest, but not lensed SMG, to see their X-ray occupation. 
    >2. Based on the VLA observation of several SMGs, we can predict its X-ray luminosity based on their 

11. Diffuse emission from dust

    > Now most SMG were found to be compact in their dust size, is it true or just because the spatial filtering of interferometer. Combine single dish with long time interferometry. 
    >
    > 1. Maybe proposing new single dish observation (JCMT and APEX)

## AGN

1. AGN timescale issue.

   > The AGN role in starbutst galaxies. Currently it very hard to find AGN in SMG, due the dust obscuration or also because their short timescal. Repeating AGN in SMG

2. Morphology transition

   > Connecting: minor merger + size increasement + AGN Intermittence

## Cosmological evolution of baryons

1. The available molelular gas reservior is somehow consistent with cosmic star formation trend. However, the atomic gas follows the general slihtly flat trend from early Universe to local Universe. One possible issue may be the dection of atomic gas in the early Universe. 



## Local galaxies

1. High resolution observation of local galaxies with low inclination angle, seperating out the weak outflow

   > It relies on the model subtraction to reomove the strong regular rotation, so that it where the uncertainty comes from.

2. DESI has much better coverage for close pair sample than SDSS, can be a much better sample to study galaxy merger. The advantages of DESI also in the deeper image, which can even be used for statistically study the minor merger.

3. Magnetic field in local interacting galaxies

   > It is a idea come from the study of magnetized filaments in Galactic center, [Coughlin et al.](https://arxiv.org/abs/2010.13790) have proposed that the tidal disruption may also play a role for the formation of the magnetic field. So it would be interesting to search the magnetic field in the tidal disrupted galaxies.

4. Molecular gas and dust properties in super-thin galaxies

   > Super-thin galaxies were though to have very cold stellar disk and rich in atomic gas. They are dominated by dark matter in all scales of the galaxy. 

5. Red spiral

   > Red spiral may be a transient stage of changing from spiral to ellipitcals
   >
   > Offering clues about the size increasing from minor or major merger at later stage
   >
   > Testing the ALMA ACA proposal for red spiral galaxies, maybe some new sample from HI-MaNGA

## Rotational curve

Study how the rotational curve changed from Cusp to Core:

1. From Ultra Diffused Galaxy -> Ultra Compact Galaxy, study the compactness of the dark matter? 

2. Maybe a parameter to quantify the compactness of dark matter is essential?

3. The compactness of dark matter as a function of galaxy type, stellar mass, baryonic compactness, age, redshift

4. High redshift SMG? If the feedback have not affect the distribution of DM

   > It may need the evidence about how long the stellar feedback can affect the distribution of dark matter.

5. Proto-cluster, if the all the members gathered in one dark matter halo, is it possible to measure the rotational curve of the cluster by the cluster members?

   > It may not be a good idea, if the proto-cluster cannot be regarded as one fully thermalized system
   >
   > They may also be dominated by peculiar velocity, to unveil the rotational velocity, the peculiar velocity has to been removed first



6. ~~Study the rotational curve of the disk galaxy at high-z, from gravitational lensing?~~～～~~ 

   > Gravitional lensing preserve surface density, to constrain the rotational curve, we need to detect the true faint, extend region which cannot boosting by lensing

## IMBH

## Cosmology

- If the core and cusp problem favour the interaction between dark matter and the baryons, will this effect have any signals in the BAO?



## Technicals

Differential phase difference:

1. ALMACAL searching for spectral lines in the unreolved blazer center, possibe place to search for gas motion using differential phase?

Power Spectra Distribution:

1. Combining PCA and SSP least square fitting



## Others

1. Cross matching all sky Wise and Herchel with strong-lensed target found by machine learning algorithm. Targeting more high-z lensed galaxies.

# Non-astronomy

1. Deep Learning: Learning the random number? How it works or whether it works. Learn real world random number and combining several random number generators.

