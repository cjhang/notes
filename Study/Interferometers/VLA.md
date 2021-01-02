#  VLA

Field of view in arcsin $\theta_{\rm\scriptsize PB} = 45'/v_{\scriptsize\rm GHz}$



Very Large Array

Sensitivity 

$\Delta I_m = \frac{\mathrm{SEFD}}{\eta_c\sqrt{n_{pol}N(N-1)t_{int}\Delta\nu}}$,   $\mathrm{SEFD} = 5.62 T_{sys}/\eta_A $

$\eta_A$: aperture efficiency, 

$\eta_c$: correlator efficiency, ~0.93 for 8-bit samplers

$n_{pol}$: number of polarization







VLA Technical Basic:

Configurations: 

| Configuration | Baseline (km) | Cycle Time (scan < 10min) |
| ------------- | ------------- | ------------------------- |
| A             | 0.68~36.4     | 10-15 min                 |
| B             | 0.21~11.1     | 20-25 min                 |
| C             | 0.035~3.4     | 30-40 min                 |
| D             | 0.035~1.03    | 50-60 min                 |

Bands:

| Band      | Frequency Range | SEFD (Jy) | Opacity  |
| --------- | --------------- | --------- | -------- |
| 4m        | 58~84 MHz       |           |          |
| P (90cm)  | 230~470 MHz     | 2790      |          |
| L (20cm)  | 1~2 GHz         | 420       | < 0.01   |
| S (13cm)  | 2~4 GHz         | 370       |          |
| C (6cm)   | 4~8 GHz         | 310       | < 0.01   |
| X (3cm)   | 8~12 GHz        | 250       | < 0.01   |
| Ku (2cm)  | 12~18 GHz       | 320       |          |
| K (1.3cm) | 18.0~26.5 GHz   | 500       | 0.05~0.2 |
| Ka (1cm)  | 26.5 ~ 40 GHz   | 600       |          |
| Q (0.7cm) | 40 ~ 50 GHz     | 1300      |          |

Notes:

1. Robust weighting, sensitivity 1.2 times worse 





**Band Synthesized Beam width $θ_{HPBW}$ (arcsec)**

| Configuration | A     | B    | C    | D    |
| ------------- | ----- | ---- | ---- | ---- |
| 74 MHz (4)    | 24    | 80   | 260  | 850  |
| 350 MHz (P)   | 5.6   | 18.5 | 60   | 200  |
| 1.5 GHz (L)   | 1.3   | 4.3  | 14   | 46   |
| 3.0 GHz (S)   | 0.65  | 2.1  | 7.0  | 23   |
| 6.0 GHz (C)   | 0.33  | 1.0  | 3.5  | 12   |
| 10 GHz (X)    | 0.20  | 0.60 | 2.1  | 7.2  |
| 15 GHz (Ku)   | 0.13  | 0.42 | 1.4  | 4.6  |
| 22 GHz (K)    | 0.089 | 0.28 | 0.95 | 3.1  |
| 33 GHz (Ka)   | 0.059 | 0.19 | 0.63 | 2.1  |
| 45 GHz (Q)    | 0.043 | 0.14 | 0.47 | 1.5  |
**Band Largest Angular Scale $θ_{LAS}$ (arcsec)**

| Configuration | A               | B              | C                   | D            |
| ------------- | --------------- | -------------- | ------------------- | ------------ |
| 74 MHz (4)    | 800             | 2200           | 20000               | 20000        |
| 350 MHz (P)   | 155             | 515            | 4150                | 4150         |
| 1.5 GHz (L)   | 36              | 120            | 970                 | 970          |
| 3.0 GHz (S)   | 18              | 58             | 490                 | 490          |
| 6.0 GHz (C)   | 8.9             | 29             | 240                 | 240          |
| 10 GHz (X)    | 5.3             | 17             | 145                 | 145          |
| 15 GHz (Ku)   | 3.6             | 12             | 97                  | 97           |
| 22 GHz (K)    | 2.4             | 7.9            | 66                  | 66           |
| 33 GHz (Ka)   | 1.6             | 5.3            | 44                  | 44           |
| 45 GHz (Q)    | 1.2             | 3.9            | 32                  | 32           |



| Configurations | Observing  Bands  | Default  integration time |
| -------------- | ----------------- | ------------------------- |
| A, B, C, D     | P                 | 2 seconds                 |
| A              | L S C X Ku K Ka Q | 2 seconds                 |
| B              | L S C X Ku K Ka Q | 3 seconds                 |
| C, D           | X Ku K Ka Q       | 3 seconds                 |
| C, D           | L S C             | 5 seconds                 |

Time average loss:

| Configuration | 1.0% | 5.0%  | 10.0% |
| ------------- | ---- | ----- | ----- |
| **A**         | 2.1  | 4.8   | 6.7   |
| **B**         | 6.8  | 15.0  | 21.0  |
| **C**         | 21.0 | 48.0  | 67.0  |
| **D**         | 68.0 | 150.0 | 210.0 |



Observation workflow:

0. 10~12 min for start-up sequency

1. Pointing scans: 
   - Typically done at X-band (8 GHz) continuum observation on strong (> 0.3 Jy/beam) with 20 degree. Main goal of pointing scans is to reach high SNR at a short integration time.
   - Need to be calibrated after a significant time of observation, every 30~40 min (daytime), 1hour (nighttime)
   - Nighttime pointing is about 10 arcsec, while occasionally exceeding 10 arcmin in the daytime due to solar heating of antennas  
- After a large distance to flux density and bandpass calibrator (> 20 º)
  
2. Phase 

2. Spectral line observation
   1. Bandpass calibrator integration time demand: $S_{cal} \sqrt{t_{cal}} > 2 S_{obj}\sqrt{t_{obj}}$
   2. Gain calibrator, the same setup for science target
   3. Frequency resolution: 4 factors of over-sampling, at 2 factors
3. 







Observational guid:

1. Avoiding shadowing: D configuration > 40º, C configuration > 25º
2. Avoiding wrap: cable length ±265º
3. Higher frequency observation need more frequent visit to the phase calibrator. Phase calibrator should avoid the sun and sunrise and sunset.
4. High frequency needs a close-by flux calibrator, as the flux density bootstrapping will introduce considerable errors if for frequency larger than 15GHz
5. Phase change more rapidly than amplitude, larger base line suffer from more rapid change in phase
6. Avoid observing L and S band during daytime, include sunrise and sunset, the ionosphere is the main contributor for phase variation 





## Useful Hints

- Integration time limitation: Limited by number of channels and maximum data rate and volume
- Doppler shift estimate: 1MHz ~ x km/s at wavelength of x in mm
- Channel frequency width is not the final spectral resolution in data-cube, which actually depends on the data process (Hanning smooth) and the weather
- Smaller source-calibrator angular separation, the better. For low frequencies(L band below), the nearby S code calibrator is better than a distant P code. While for higher frequency, higher quality P-code 

1. For higher frequency, a closer complex gain calibrator is better than a stronger but far away one. However, for low-freqeucny observation L, S, C, X-band, it is suggested to choose a P calibrator, rather than a weaker nearby weaker S source.





Questions:

1. Bandpass calibrator: if broad RFI occurs, the slightly off in frequency and transfer to target frequency?
2. Gain calibrator: different bandwidth can introduce a phase offset ? A strong source at both setup
3. Band and sub-band, 8-bit sampler and 3-bit sampler
4. Tipping scans: measure atmospheric opacity
5. Cycle time vs bracketing?