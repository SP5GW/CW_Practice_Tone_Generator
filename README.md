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

$Uc(t)[V] = (Uhigh[V] - Un[V])(1-e^{\left(-\frac{t[sec]}{R[ohm]*C[F]}\right)}) + Un[V]$ *)

where:

$Uc(t)$ - Voltage across the capacitor at time t

$Uhigh$ - The supply voltage (or maximum voltage the capacitor will eventually charge to - in  our case theoretically)

$Un$ - The voltage level at which the Schmitt trigger output switches from low to high

$t$ - Time since charging began

$R$ - Resistance in the circuit (in ohms)

$C$ - Capacitance of the capacitor (in farads).


To calulate time it takes for capacitor voltage to reach Uc(t)=Up, we solve equation *) for t = th (i.e. th is a time instance when Uc(t) reaches Up)

$Up = (Uhigh - Un)(1-e^{\left(-\frac{th}{R*C}\right)}) + Un$

$\frac{Up - Un}{Uhigh - Un} = 1-e^{\left(-\frac{th}{R*C}\right)}$

$1 - \frac{Up - Un}{Uhigh - Un} = e^{\left(-\frac{th}{R*C}\right)}$

$\ln{(1 - \frac{Up - Un}{Uhigh - Un})} = \ln{e^{\left(-\frac{th}{R*C}\right)}}$

$-\frac{th}{R*C} = \ln{(1 - \frac{Up - Un}{Uhigh - Un})}$

$-th = R*C \ln{(1 - \frac{Up - Un}{Uhigh - Un})}$ 

$th = -R*C \ln{\frac{Uhigh - Un - Up + Un}{Uhigh - Un}}$

$th = -R*C \ln{\frac{Uhigh - Up}{Uhigh - Un}}$ 

from reciprocal rule $-\ln{x} = \ln{\frac{1}{x}}$, which in our case produces:

$th = R*C \ln{\frac{Uhigh - Un}{Uhigh - Up}}$


Similarly, the capacitor voltage during its discharging phase can be expressed as:

$Uc(t)[V] = Up*e^{(-\frac{t[sec]}{R[ohm]*C[F]})}$ **)

where:

$Uc(t)$ - Voltage across the capacitor at time t

$Uhigh$ - The supply voltage (or maximum voltage the capacitor will eventually charge to - in  our case theoretically)

$Up$ - The voltage level at which the Schmitt trigger output switches from high to low

$t$ - Time since charging began

$R$ - Resistance in the circuit (in ohms)

$C$ - Capacitance of the capacitor (in farads).

To calulate time it takes for capacitor voltage to reach $Uc(t)=Un$, we solve equation **) for $t = tl$ (i.e. $tl$ is a time instance when $Uc(t)$ drops from $Up$ to $Un$)


$Uc(t)[V] = Up*e^{(-\frac{t[sec]}{R[ohm]*C[F]})}$

$Un = Up*e^{(-\frac{tl}{R*C})}$

$\frac{Un}{Up} = e^{(-\frac{tl}{R*C})}$

$ln{\frac{Un}{Up}} = ln{e^{(- \frac{tl}{R*C})}}$

$-\frac{tl}{R*C} = ln{\frac{Un}{Up}}$

$tl = -R*C ln{\frac{Un}{Up}}$

from reciprocal rule $- \ln{x} = \ln{\frac{1}{x}}$, which in our case produces:

$tl = R*C ln{\frac{Up}{Un}}$

The period of the oscillator's output signal can be expressed as:

$T = th + tl$

Using formulas for $th$ and $tl$ dervied earlier we can express $T$ as:

$T = R*C \ln{\frac{Uhigh - Un}{Uhigh - Up}} + R*C \ln{\frac{Up}{Un}}$

$T = R*C [\ln{\frac{Uhigh - Un}{Uhigh - Up}} + \ln{\frac{Up}{Un}}]$