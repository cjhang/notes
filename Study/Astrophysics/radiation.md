

# Basics

## Intensity and its moments

$$dE_\nu = I(x,\hat{n},\nu,t)\hat{n}\cdot\hat{k}\,d\nu\,d\Omega\,dA\,dt $$ 

- $I$ is specific intensity, mostly written in $I_\nu$ , with an units of  [$\text{erg}\,s^{-1}\,cm^{-2}\,sr^{-1}\text{Hz}^{- 1}$] or [$\text{W}\,m^{-2}sr^{-1}\text{Hz}^{-1}$]
- x is the coordinate, $\nu$ is frequency and t is time
- $\hat{n}$ is the direction of intensity, it is variable
- $\hat{k}$ is the direction of interest, it is fixed
- Intensity can be taken as a flow of radiation



### Moment 0

$J(x,\nu, t) = \frac{1}{4\pi}\int I(x,\hat{n},\nu,t)\text{dΩ}$

- 0th moment is a scalar, stands for the **mean intensity**, it has the units of [$\text{erg}s^{-1}cm^{-2}\text{Hz}^{-1}$]
- if the source is isotropic, then $I_\nu = J_]\nu$
- Energy density $u = 4\pi J/c$, with units: [$\text{erg cm}^{-3}$\], it is the radiative energy per unit volume

### Moment 1

$F_{v} = \int I(x,\hat{n},\nu,t)\hat{n}\,d\Omega = \int I_\nu \cos\theta d\Omega$ 

- $F_\nu$ is called flux density,  it is net flow of energy, it has the units of [${\rm erg\,s}^{- 1}\text{cm}^{-2}\text{Hz}^{- 1}$]
- $F_\nu$ is a vector, usually in the direction we inetered. For isotrpic source, all the solid integration result in 0

- the source is resolved, $F_{v}$ is almost constant (if object is

  - intensity is constant, as the solid angle is always the same
  - the source is unresolved, $F_{v}$ decreace with distance as $1/r^{2}$, since $F=\frac{L}{4\pi r^2}$

-   If we only account the flux in one direction, for black body we have: 

    $$F_\nu^+ = B_\nu\int_{\theta=0}^{\pi/2}\int_{\phi=0}^{2\pi}\cos\theta\sin\theta d\theta d\phi = \pi B_\nu$$

    In this case, $B_\nu$ is intensity while $\pi B_\nu$ is flux

### Moment 2

$P(\bold{x},\nu,t) = \frac{1}{c}\int I(x,\hat{n},\nu,t)\,\hat{n}\hat{n}\,\text{dΩ}$

$P_{kk,\nu} = \frac{1}{c}\int I_\nu \cos^2\theta\,d\Omega$

- $P_\nu$ is called radiation pressure, it is a tensor.
- if the source is isotropic, $P_\nu = \frac{4\pi}{3c}I_\nu$





 

## Stellar opacity

$d I_\nu = -\kappa_\nu I_\nu ds$

- $\kappa_\nu$ is called opacity, it has the units of $m^{-1}$
- $1/\kappa_\nu = \bar{l}$ is the mean-free path of radiation
- in some cases, $d I_\nu = -\kappa_\nu^m\rho I_\nu ds$,   $\kappa_\nu^m$ is called the mass opacity



Three scale:

1\. temperature scale height: $H_{T} = \frac{T}{|\text{dT}/\text{dr}|}$

2\. mean free path $l = \frac{1}{\text{nσ}} = \frac{1}{\text{κρ}}$, when
$l \ll H_{T}$ it can safely apply the LTE

3\. optical depth $\tau = \int_{0}^{s}\text{κρds}$, $\tau = 1$ can be
regard as the $s = l$

 

Opacity source

1.  bound-bound, scatter, true absorption, collide to thermal degrading radiative energy

2.  bound-free, continuum, degrading radiative

3.  free-free, bremsstrahlung

4.  electron scattering, free-electron, Thomson scattering, efficient in high temperature dense gas, loosely bound electron: Compton scattering if $\lambda > r_{\text{atom}}$, Rayleigh scattering if $\lambda < r_{\text{atom}}$

$H^{-}$ with bound energy 0.754eV (1.64𝜇m) is a important continuum
opacity of star cooler than F0

![A picture containing object Description automatically
generated](radiation.assets/image1.png){width="5.180555555555555in"
height="0.4444444444444444in"}

except $\kappa_{\text{bb}}$, other four have well calculated by average
opacity



## LTE and non-LTE

Local Thermodynamic Equilibrium (LTE): local version of thermodynamic equilibrium where temperature, pressure, and chemical gradients are small compared to the photon mean free path.