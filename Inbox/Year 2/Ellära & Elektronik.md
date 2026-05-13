# Föreläsning 1 - Definition av grundläggande begrepp
## Ström:
Ampere ($A$) är hastigheten på flödet av elektrisk laddning ($q(t)$) i Coulomb ($C$)
$$\Large
\begin{array}s
\text{Elektron: } \bar{e} = 1,6 \times 10^{-14} C \\
\text{Ström: }i(t) = \frac{dq(t)}{dt} \iff q(t) = \int_{t_0}^{t_1} i(t) dt \ + \ q_0(t) \\
\text{Likström (DC), är en konstant: } i(t) = i_0 \\
\text{Växelström (AC), ändras enligt sinus kurva: } i(t) = i_a \ \cdot \ sin(2\pi \cdot t) \\
\end{array}
$$
![[Pasted image 20260412144634.png|697]]
![[Pasted image 20260412144700.png|697]]
OBS! Ström har en referenriktning från $+$ till $-$. Skilj på algebreiska storhet och fysisk riktning.
```
i_a --> 
------[ R ]-----
         <-- i_b

i_a = -i_b
```

## Spänning:
Volt ($V$) är skillnaden mellan två punkter, potentiel skillnad
$$\Large
\begin{array}s

\text{Spänning: } V=[\frac{\text{Joule}}{\text{Coulomb}}] = \frac{Energi}{Laddning}

\end{array}
$$
## Effekt:
$P$, Watt ($W$) är då hastighet per energi
$$\Large
\begin{array}a
\text{Effekt: } \ p(t) = \frac{d \ E(t)}{d \ t} = V(t) \ \times \ i(t) \Rightarrow P = U \ \cdot I \\

[\frac{\text{Joule}}{\text{Coulpmb}} 
\times 
\frac{\text{Coulomb}}{\text{sec}} = 
\frac{\text{Joule}}{\text{sec}}
= W] \\

E(t) = \int_{t_0}^{t_1} p(t) dt
\end{array}
$$

## Resistans
Resistans ($R$, Ohm, $\Omega$) är motstånd. Dvs matrial som motsätter energi genomgång.
$$\Large
\text{Resistans: } R = \frac{\rho \cdot L}{A}
$$
* $\Large \rho =$ Materialets resistans
* $\Large L =$ Matrialets Längd
* $\Large A=$ Arean på snittet på ledaren

Motsattseb kallas konduktans, $G$, elektrisk ledningsförmåga

## Ohm's Lag
![[Pasted image 20260412145950.png]]
$$\Large
V = R \cdot i \iff
R = \frac{V}{i} \iff
i = \frac{V}{R}
$$
## Oberoende källor (generatorer)
Oberoende p.g.a. ström och spännings källor är oberoende av varandra. Strömmar och spänningen i kretsen
![[Pasted image 20260412151056.png]]

## Beroende Källor
Dvs. ström/spånnings källan är en funktion av andra ström och spänningen i kretsen
![[Pasted image 20260412151156.png]]

## Seriekoppling och Parallellkoppling

![[Pasted image 20260412151301.png]]
$$\Large
\begin{array}a
\text{Seriekoppling: } i = i_1 = i_2 = i_3 \ \text{(Samma Ström)} \\
\text{Parallelkoppling: } V = V_1 = V_2 = V_3 \text{(Samma Spänning)}
\end{array}
$$
## Kirchov's strömlag (KCL)

$\Large \sum$ strömmen in till en nod $\Large = \ \sum$ strömmen ut från en nod.

![[Pasted image 20260412152919.png]]
$$\Large
i_1 = i_2 + i_3
$$
## Kirchov's Spänningslag (KVL)

$\Large \sum$ spänningen i en sluten loop $\Large = 0$, dvs den algebraiska summan av all potentialändringar/spänningen längs en sluten väg $\Large = 0$ 

![[Pasted image 20260412153229.png]]

## Principen om beroende av Effekt/Energi
$$\Large 
\sum \text{angiven Effekt/Energi } \Large = \sum \text{absorberade Energin/Effekten }
$$
Definition:
![[Pasted image 20260412153628.png]]
```
   i +  U  -
--->--[ R ]---  => P = U * i

   i -  U  +
--->--[ R ]--- => P = -U * i

```

$$\Large
\begin{array}a
\text{om } P > 0 \Rightarrow \text{tar upp effekt} \\
\text{om } P < 0 \Rightarrow \text{avger effekt} \\
\end{array}
$$

## KCL och KVL Exempel

![[Pasted image 20260412154234.png|697]]


## Ersättnings Resistans

```
I serie:
o--->--[R_1]--[R_2]-...-[R_N]---     o---[R_T]--
                               |  =>           |
o-------------------------------     o----------

Parallellt:
o-------o-------o--...---        o---[R_T]---
	  [R_1]   [R_2]   [R_N]  =>             |
o-------o-------o--...---        o-----------
```

$$\Large
\begin{array}s
\text{Serie: } R_{T} = \sum_{i=1}^N R_i \\
\text{Parallelt: } \frac{1}{R_T} = \sum_{i=1}^{N} \frac{1}{R_i}
\end{array}
$$
![[Pasted image 20260412165626.png]]

## Ersättnings konduktans
Konduktans, $G$, motsats till resistans:
$$\Large
\begin{array}s
G = \frac{1}{R} \\
\text{I Serie: } \frac{1}{G_{eq}} = \sum_{i=1}^N \frac{1}{G_i} \\
\text{I Parallelt: } G_{eq} = \sum_{i=1}^N G_i
\end{array}
$$
![[Pasted image 20260412170045.png]]

## Kretsanalys med ekvivalent resistansen (Metod)
1. Förenkla så långt som möjligt med hjälp av serie/parallelt eqvivalenter. Idealt får man då en källa och en resistans.
2. Lös den eqvivalenta kretsen m.h.a. KCL, KVL, Ohm's Lag.
3. Gå tillbaka ett steg och lös de saknade variablerna. Uppreppa tills de kommer tillbaka till den ursprungliga kretsen.
4. Kontrollera att KCL, KVL fortfarande gäller!

![[Pasted image 20260412170353.png|697]]

---
# Föreläsning 2

## Spänningsdelning (Serie)

![[Pasted image 20260412171446.png]]

## Strömdelning (parallell)

![[Pasted image 20260412171526.png]]

## Nodanalys

![[Pasted image 20260412172016.png|697]]

1. Välj en referens nod och jorda, dvs, inför en beräkningsjord potential $\Large = 0$.
2. Ange nodspänning $\Large V_1,\ V_2,\ V_3$, som obekant.
3. Kan någon av nodspänningarna bestämmas direkt?
4. Skriv KCL ekvationer i övriga noder m.h.a. nodspänningar, dvs KCL för resistor strömmen. Anta alltid utgående strömmen från nod. Då blir det rätt tecken till slut.
5. Sätt upp ekvationer i standard form (seperera nodspänning)
6. Lös ekvationsystemet genom $\Large V = G^{-1} I$ för att erhålla nodspänningarna. M.h.a. nodspänningarna bestäms sedan strömriktningarna!

Exempel för Nodanalys:

![[Pasted image 20260412172823.png]]

## Tvåpol
En tvåpol är en komponent eller koppling av flera komponenter som är försed med tvåpolen för anslutning till elkrets.

![[Pasted image 20260412173124.png]]

## Tvåpoler karäkteristik

![[Pasted image 20260412173203.png]]

## Spännings Tvåpol (Thévenin)

![[Pasted image 20260412173255.png]]

* $\Large V_T$  är ekvivalent till den öppna kretsens spänning i den ursprungliga kretsen
* Om vi korstluter polerna $\Large a \ \& \ b$, måste strömmen, $\Large i_T$ vara ekvivalent till kortslutningsströmmen i den ursprungliga kretsen, $\Large i_{sc}$ (short-circuit, kortslutnings ström)
* Därför: 
$$\Large
R_T = \frac{V_T}{i_T} = \frac{V_{oc}}{i_{sc}}
$$
## Spännings Tvåpol Exempel

![[Pasted image 20260412173729.png|697]]

## Ström Tvåpol (Norton)

![[Pasted image 20260413104114.png]]

* Om vi kortsluter terminalerna a & b, så blir kortslutningsströmmen $I_{SC} = I_N$, dvs spänningen över $R_T, V_T =0$
* Ström tvåpol kan bestämmas på samma sätt som får Spännings tvåpol, dvs bestämma $V_{OC}, \ I_{SC}, \ R_N$.
* Det råder ekvivalens mellan spännings tvåpol och ström tvåpol.

![[Pasted image 20260413104518.png]]

## Superpositionsprincipen

Ex. En krets har flera oberoende källor.

Kretsens beteende är summan av bidraget från varje enskild källa. Det betyder att vi kan nollställa alla källor utom en för att beräkna bidraget. Upprepa för varje källa och summer för totala kretsens beteende. Detta gäller endast för kretsens betende. Detta gäller endasbt för krestsen med linjärt beteende.

![[Pasted image 20260413110400.png]]

## Wheatstone brygga

![[Pasted image 20260413110431.png]]

---

# Föreläsning 3 - Kondensator

![[Pasted image 20260413110633.png]]

$$ \Large
\begin{array}a
C = \frac{\xi \cdot A}{d} \\
C = \text{kapacitans} \\
\xi = \text{isolatorns isolationföremål} \\
A = \text{Area} \\
d = \text{avstånd}
\end{array}
$$

1. Storleken på laddningen är propotionell till spänningen som ligger mellan platform laddning $q$ är: $q(t) = C \cdot U_c(t)$ 

2. Derivera uttrycket m.a.p. tiden $t$: 
$$\Large 
\frac{d \ q(t)}{d \ t} = \frac{d}{d \ t} C \cdot U_c(t) \Rightarrow i ± C \ \frac{d \ U_c(t)}{d \ t}
$$
	OBS! I stationära tillstånd är kondensatorn ett avbrott, dvs ingen ström.

3. Enheten på kapasitens är Farad($F$), 1 Farad är en mycket stor kapasitans

4. Berärkning av laddning och spänning i kondensatorn givet strömmen, dvs integrerar strömmen för att få laddning: 
$$\Large
	q(t) = \int_{t_0}^{t} i(t)dt + q_o(t) \Rightarrow i= \frac{d\ q(t)}{d \ t} $$
	Insättning av $q(t)=C\cdot U_c(t)$ i ovan ger:
$$\Large
U_c(t) = \frac{1}{C} (\int_{t_0}^{t} i(t) dt \ + \ q_0(t))
$$
	Ju större kapasitans desto mer ström går det åt för att ladda upp en viss spänning.

5. Effekten, avgiven/absorberad, av kondensatorn 
$$\Large 
P(t) = U(t) \ \cdot \ i(t) = U_c(t) \ \cdot \ C \ \cdot \frac{d \ U_c(t)}{d \ t}
$$
	OBS! om derivatan är noll $\Rightarrow P = 0$, dvs trivs en förändring av spänningen.

6. Energin som lagrats i kondensatorn.
$$\Large
\begin{array}a
W(t) = \int_{t_0}^t P(t)\  dt \\
W(t) = \int_{t_0}^t C \ \cdot \ U_c(t) \ \cdot \ \frac{d \ U_c(t)}{d\ t} \ d \ t  \\
W(t) = \int_{t_0}^t C \ \cdot \ U_c(t) \ \cdot \ d \  U_c(t)  =\\
C[\frac{U_c^2(t)}{2}]_0 ^{U_c(t)} = C \ \cdot \ \frac{U_c^2(t)}{2}
\end{array}
$$
	Energi vid en viss tidpunkt.

## Parallellkoppling av kapcitenser

![[Pasted image 20260413131825.png|697]]

$$\Large
\begin{array}a
q = C_{eq} \ \cdot \ U = C_1 \ \cdot \ U \ + \ C_2 \ \cdot \ U \ + \ ... \ +\ C_n \ \cdot \ U \\
C_{eq} = \sum_{i=1}^N C_i
\end{array}
$$

## Seriekoppling av kapacitenser

![[Pasted image 20260413131924.png|697]]
$$\Large
\begin{array}a
U = \frac{q_s}{C_{eq}} = \frac{q_s}{C_1} + \frac{q_s}{C_2} + \ ... \ + \frac{q_s}{C_N} \\

\Rightarrow \frac{1}{C_{eq}} = \sum_{i=1}^N \frac{1}{C_i}
\end{array}
$$
## Parecit effekten
En verklig kapasitens har paresitisk effekter och induktens, dvs.

![[Pasted image 20260413132433.png|519]]

## Induktor (Spole)
Exempel filter, lagra energi, elmotor,  generatorn transformetor.

![[Pasted image 20260413132711.png|469]]

* När en **likspänning** läggs över en spole begränsas strömmen precis som en resistor. Strömmen kan beräknas med Ohm's Lag
* Om strömmen varierar uppträder också en annan typ av motor