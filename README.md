# CW_Practice_Tone_Generator

<p align="center">
<img src="./img/outside_v2.jpg" width="600" height="600"/>
</p> 

## Project overview

This project is a result of very real need to be able to practice when learning CW. There are many CW tone generator kits and reference designs on the internet, however I have not found one, which would allow connecting both speaker and head phones. Desings found on the internet also did not have volume control. 
When designing this project I was inspired by work described in [1] and [2].

It is not essential for this project to understand in detail how single Schmitt gate oscillator works, but if you are interested you will find all formulas and measurements in Appendix 1. 

Device schematics:

<p align="center">
<img src="./img/CW_Practice_Tone_Generator_Schematics.png" width="800" height="600"/>
</p>

Device internals:

<p align="center">
<img src="./img/internals_main.jpg" width="250" height="250"/>
<img src="./img/internals_pcb.jpg" width="250" height="250"/>
<img src="./img/internals_key_volume_pot.jpg" width="250" height="250"/>
<img src="./img/internals_headphones_jack.jpg" width="250" height="250"/>
</p>


## References

[1] [Generator Tonu by Radiohobby.pl](<https://radiohobby.pl/projekty/generator-tonu/>)

[2] [More Code Tone Generator Using the 4093 IC (ART159E)](<https://incbtech.com/index.php/articles/9-projects/642-morse-code-tone-generator-using-the-4093-ic-art159e>)

[3] [Exactly How Schmitt Trigger Oscillators Work by Eduardo Corpeno](<https://www.allaboutcircuits.com/technical-articles/exactly-how-schmitt-trigger-oscillators-work/>)

## Appendix 1 - Understanding Oscillator Design


<p align="center">
<img src="./img/fmin_Uout_Timing_1_commented.png" width="400" height="400"/>
<img src="./img/fmin_Uc_Levels_Commented.png" width="400" height="400"/>
</p>

Capacitor voltage during its charging phase can be expressed as:

$Uc(t)[V] = (Uhigh[V] - Un[V])(1-e^{\left(-\frac{t[sec]}{R[ohm]*C[F]}\right)}) + Un$ *)

where:

$Uc(t)$ - Voltage across the capacitor at time t

$Uhigh$ - The supply voltage (or maximum voltage the capacitor will eventually charge to - in  our case theoretically)

$Un$ - The voltage level at which the Schmitt trigger output switches from low to high

$t$ - Time since charging began

$R$ - Resistance in the circuit (in ohms)

$C$ - Capacitance of the capacitor (in farads).

To calulate time it takes for capacitor voltage to reach Uc(t)=Up, we solve equation *) for t = th (i.e. th is a time instance when Uc(t) reaches Up)

$(Up - Un) = (Uhigh - Un)(1-e^{\left(-\frac{th}{R*C}\right)})$

$\frac{Up - Un}{Uhigh - Un} = 1-e^{\left(-\frac{th}{R*C}\right)}$

$1 - \frac{Up - Un}{Uhigh - Un} = e^{\left(-\frac{th}{R*C}\right)}$

$\ln{(1 - \frac{Up - Un}{Uhigh - Un})} = \ln{e^{\left(-\frac{th}{R*C}\right)}}$

$-\frac{th}{R*C} = ln{(1 - \frac{Up - Un}{Uhigh - Un})}$

$-th = R*C*\ln{(1 - \frac{Up - Un}{Uhigh - Un})}$

$th = -R*C*\ln{\frac{Uhigh - Un - Up + Un}{Uhigh - Un}}$

$th = -R*C*\ln{\frac{Uhigh - Up}{Uhigh - Un}}$

from reciprocal rule $-\ln{x} = \ln{/frac{1}{x}}, which in our case produces:

$th = -R*C*\ln{\frac{Uhigh - Un}{Uhigh - Up}}$


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



