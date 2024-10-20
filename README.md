# CW_Practice_Tone_Generator

<p align="center">
<img src="./img/outside_v2.jpg" width="600" height="600"/>
</p> 

## Project overview

xxx


## References

[1] [The definitive guide to RF Power measurement](<https://qrp-labs.com/qcx/rfpower.html>)

[2] [Is It OK to Use an External 50 Ohm Terminator with an Oscilloscope?](<https://blog.teledynelecroy.com/2022/06/is-it-ok-to-use-external-50-ohm.html>)

## Appendix 1 - Understanding Oscillator Design


<p align="center">
<img src="./img/Sinwave.jpg" width="600" height="400"/>
</p>

where:

$Upp$ - Peak to Peak Voltage

$Up$ - Peak Voltage

$Up = Upp / 2$

Both, $Up$ and $Upp$ can be directly read from the scope screen.

$Urms$ - Root Mean Square Voltage 

For a periodic AC voltage, the $Urms$ value represents the equivalent DC voltage that would deliver the same amount of power to a resistive load.

In case of sinusoidal waveform specifically, the RMS voltage can be expressed as:

$Urms = \frac{Up}{\sqrt{2}}$        (*)

### Power

Power is the measure  of the energy per unit of time transfered by the electric circuit and can be expressed as:

$P=U \times I$      (**)

From Ohm's law:

$R=U \times I$, 

which gives:

$I= U \times R$ 

If we substitute I in equation (**) with equation for I derived from Ohm's law above, we get the formula expressing power dicipating on the load R:

$P = \frac{U^2}{R}$

In RF measurements we sometime discuss peak power, which is the maximum instantaneous power that a system can deliver or consume at any given moment:

$Pp = \frac{Up^2}{R}$

and even more often average power, representing the consistent power output or consumption over time. 

In case of sine waveform, average power can be expressed as:

$Pavg = \frac{Urms^2}{R}$

$Urms$ is not directly visible on the screen of osciloscope. That is why we need to convert above formula by substituting $Urms$ with formula (*), which gives:

$Pavg = P = \frac{Up^2}{2 \times R}$

RF Power Output listed in radio equipment specifications refers to average power. That is why for simplicity we will refer to average power as power.

### Finding peak voltage coresponding to given power Level 

Other useful equations, allow to find peak voltage $Up$ on load R for given power or peak power level:

$Up = \sqrt{2 \times P \times R}$

or

$Up = \sqrt{Pp \times R}$


### Converting power between dBm and Watts

To convert power given in dBm to Watts we use:

$P[W] = 10^{\left(\frac{P[dBm]}{10} - 3\right)}$

To convert power given in Watts to dBm we use:

$P[dBm] = 10 \times \log{\frac{P[W]}{0,001}}$




$[dBm] = 10 \times \log{\frac{P2[W]}{0,001W}}$

We can calculate the relation between power ratio and equivalent voltage ratio on given load R as:

$10 \times \log{\frac{P2[W]}{P1[W]}} = 10 \times \log{\frac{\frac{(U2[V])^2}{R}}{\frac{(U1[V])^2}{R}}} = 10 \times \log{(\frac{U2[V]}{U1[V]})^2}  = 20 \times \log{\frac{U2[V]}{U1[V]}}$

As can be seen from the above, the relation expressed in logarythmic scale between ratios of power and coresponding voltage ratios on given load is:

$10 \times \log{\frac{P2[W]}{P1[W]}} = 20 \times \log{\frac{U2[V]}{U1[V]}}$     (***)

In practice this means that if use attenuator, which attenuates power by -40dB, the coresponding voltage attenuation will be equal to:

$Att[dB] = 10 \times \log{\frac{P2[W]}{P1[W]}} = -40dB$

then from (***):

$\frac{U2}{U1} = 10^{(\frac{Att[dB]}{20})} = 10^{-2} = 0.01$ (!)



