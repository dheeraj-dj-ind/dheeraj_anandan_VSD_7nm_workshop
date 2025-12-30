# Introduction
This is a 10-day workshop on "FinFET Circuit Design and Characterization using ASAP7 PDK" carried out by VSDIAT. This focuses on FinFETs, mainly the asap7nm opensource technology where we characterize a NMOS transistor, inverter circuit using the asap7nm node. The document also comprises a brief introduction to FinFETs and the journey from large gate sized, to sub 1nm nodes. The duration of this workshop is from 26th Dec to 4th Jan.

# 1. History of Transistors 
![large systems to cmos](images/Screenshot%202025-12-26%20123713.png)

## 1.1 Microprocessor trend 
![MP trend](images/Screenshot%202025-12-26%20124059.png)

## 1.2 Path to Zeta Scale Computing 
![Zeta scale](images/Screenshot%202025-12-26%20124705.png)

## 1.3 CMOS Evolution 
- Beyond a certain node size, Denard scaling was observed to be deifficult to follow, thus causing device scaling to include next geeration innvoations such as Patterning, using different Channel Material, Gate Stack, Interconnection Material, Device Architecture, Chiplet/3D integration. 
![elolution](images/Screenshot%202025-12-26%20125006.png)

## 1.4 Introduction to FinFETs
FinFETs are a type of field effective transistor that has a fin like structure rather than being completely planar. The gate wraps around the fin on all three side, which connect to the source and drain terminals of the device. FinFETs came into play in the early 2010s when planar transistors could not be scaled down below 30nm due to short-channel effects. These devices proved to have enchanced `gate controll, faster switching speeds, increased drive current` all at a low supply voltage (VDD).

![FinFETs](images/Screenshot%202025-12-26%20135609.png)

![double gate](images/Screenshot%202025-12-26%20150657.png)

### 1.4.1 Why FinFETs

1) Short Channel Effects
- In a planar CMOS below 30nm gate length, as Vds increases, the potential barrier around the gate starts to grow. In short channel devices, as the potential barrier of gate increases, there is a high chance for it to overlap the potential barrier of source terminal. 
- This causes charges to flow in absence of Gate control called as Drain Induced Barrier Leakage (DIBL) and increased threshold voltage (Vt).
FinFETs on the other hand are double gated or tri gated structures that supress short channel effects 

2) Reduced Leakage and Faster Switching
- Compared to planar CMOS, FinFETs have improved subthreshold swing (ability to turn on and off quicker) as the gate controlls the channel from multiple directions.
- Subthreshold swing is directrly proportional to (1+Cd/Cox)
- As a result, the static leakage current is also reduced.

3) Enhanced Drive Current 
- The introduction of fin in transistors, cause a change in the effective width of device, where Weff = 2Hfin + Tfin
Hfin is the height of fin and Tfin is the thickness of fin. 
- With increase in fin height along with multiple fins in place, the transistors drive current density increases significantly.

4) Power Efficiency
- FinFETs have observed to have lower dynamic and static leakage currents at the same threshold voltage (Vt) as that of planar transistors. This leads to improved power efficiency (P∝CV2f)
- At the same leakage current as planar devices, FinFETs observe lower Vt which translates to a lower suppy voltage Vdd. 

![leakage](images/Screenshot%202025-12-26%20151053.png)

5) Reduced Variablity
- The variability in planar transistors started to increase because doping concentration in channel increased.
- With the introduction to FinFETs, variability started to drop as they displayed better channel control as it is made of less doped channels. 

![variability](images/Screenshot%202025-12-26%20183324.png)

## 1.5 Front End of Line Inovations
FEOL innovations affected design rules changes that resulted in modified ways to lay down the standard cells in a chip. 

### 1.5.1 CMOS Technology Inflection Points
- Moore's law does not specify the performance of IC's as no. of transistors increase on a chip. However Bob Denard came up with a methodology to predict the performance of a transistor by figuring out the supply voltage at a given gate lenght. 

![inflection points 1](images/Screenshot%202025-12-26%20164849.png)
![Inflection points 2](images/Screenshot%202025-12-26%20175916.png)

- Devices of size in range ~1 µm to 180 nm followed Denards scaling i.e. supply voltage scaling.
- 130 nm - The BEOL RC was affected and Aluminim BEOL was too resistive so Copper interconnects were introduced. 
- 90 nm - uniaxial strained Si NMOS 
- 65nm - Introduction to Ultra Low K Dielectric to minimize BEOL RC
- 45 nm - In HKMG transistors, a polysilicon doped gate is replaced by a metal gate to reduce electrical oxide thickness and gate leakage. 
- 32 nm - Observed a second generation HK MG which notriced that random variation went down substantially. 
- 22 nm - FinFETs were introduced. More powerful compared to previous generation transistors due to improved gate control and 3D nature. 
- 14 nm - Single diffusion break was introduced along with SADP that reduces pitch by 2, helping in redction of cell height. 
- 10 nm - Transistioned from gate contact being on the STI to gate contact being on the active regions. Moved onto bi-directional litho edge (LELELE) where printing was done in three different steps.
- 7 nm - introduction of EUV, which is a single patterned lithograpgy compared to multi-pattern lithograpgy cone with LELELE.
- 5 nm - Significant change in channel material. PMOS was made of SiGe fin that had higher mobility than Si channel. 
- 3/2/1.4 nm - Introduction to GAA/nanosheet. Channel thickness on vertical side can be controlled much easier that chaneel thickness done by lithography on horizontal side. 
- Sub 1 nm - Introduction to Conplementary FET architecture. Use of different 2D material to reduce source to drain tunneling such as MoS2. 

### 1.5.2 Standard Cell Area Scaling
![fin depopulation](images/Screenshot%202025-12-26%20180008.png)
![diff break](images/Screenshot%202025-12-26%20181417.png)

### 1.5.3 Parasitic Resistance
![para resistance](images/Screenshot%202025-12-26%20215628.png)
![para resistance 2](images/Screenshot%202025-12-26%20215642.png)

### 1.5.4 Parasitic Capacitance
![para cap](images/Screenshot%202025-12-26%20220844.png)

### 1.5.5 Device Scaling


# 2. Simulation of Inverter Using asap7nm Technology
For the simulation process, we will be using the opensource spice simulator - NgSpice and schematic viewr - Xschem. 

## 2.1 NFET Characterization
The spice deck used for characterization of nfet is [NFET SPICE](./nfet_char.spice)

- NFET schematic 

![scehmatic](images/Screenshot%20from%202025-12-27%2014-46-04.png)

- Id vs Vgs 

![id vs vgs](images/Screenshot%20from%202025-12-27%2014-30-30.png)

- Id vs Vd

![Id vs Vd](images/Screenshot%20from%202025-12-27%2014-31-03.png)

## 2.2 Inverter Characteristics using 7nm FinFETs
The spice deck using for characeterizing the inverter is [SPICE Deck](./attachments/inverter_vtc.spice)

- NgSpice console output 

![spice window1](images/Screenshot%20from%202025-12-27%2018-04-40.png)
![spice window2](images/Screenshot%20from%202025-12-27%2018-05-20.png)

- DC Analysis: VTC Curve (Vin vs Vout)

![VTC](images/Screenshot%20from%202025-12-27%2017-43-56.png)

```bash 
meas dc v_th when nfet_out=nfet_in
plot nfet_out nfet_in
```

- DC Analysis: vol, voh, vil, vol, Noise Margins
```bash 
meas dc vil find nfet_in when gain_av = gain_target cross = 1
meas dc voh find nfet_out when gain_av = gain_target corss = 1
meas dc vih find nfet_in when gain_av = gain_target cross = 2
meas dc vol find nfet_out when gain_av = gain_target cross = 2
let NMH = voh - vih
let NML = vil - vol
print v_th max_gain vil voh vih voll NMH NML
```

- DC Analysis: Drain Current
```bash 
let id = v2#branch
plot id
```

![Id curve](images/Screenshot%20from%202025-12-27%2017-43-38.png)

- DC Analysis: Transconductance (Gm)

```bash 
let gm = real (deriv(id,nfet_in))
meas dc gm_max MAX gm
plot gm
```

![transonductance](images/Screenshot%20from%202025-12-29%2009-59-53.png)

- DC Analysis: Output Impedance (r_out)

```bash
let r_out = deriv(nfet_out,id)
plot r_out
```

![r_out](images/Screenshot%20from%202025-12-27%2017-43-46.png)

- Transient Analysis: Input and Output Waveforms

![transient output](images/Screenshot%20from%202025-12-29%2010-46-29.png)

- Transient Analysis: Rise time, Fall time, Frequency

```bash
tran 0.1 100p
meas tran tr when nfet_in=0.07 rise = 1
meas tran tf when nfet_out=0.63 fall = 1
let t_delay = tr + tf
print t_delay
let f = 1/t_delay
print f
```

- Transient Analysis: Propogation Delay

```bash 
meas tran tpr when nfet_in = 0.35 rise = 1
meas tran tpf when nfet_out = 0.35 fall = 1
let tp = (tpr + tpr)/2
```

- Transient Analysis: Transient Power

```bash
let trans_current = v2#branch
meas tran id_pwr integ trans_current from=2e-11 to=6e-11
let pwr = id_pwr * 0.7
let power = abs(pwr/40e-12)
```

![transient current](images/Screenshot%20from%202025-12-29%2010-00-52.png)

## 2.3 Assignment 
The assignment given was to find characteristics of an inverter over a range of number of fins for both NMOS and PMOS in a inverter circuit. By using a loop, an excel spread sheet is created varrying Nfin_N and Pfin_N from 7 to 21, with a unique voltage `Vuniq`. The spice code is given below

- [SPICE Deck](attachments/inverter_vtc_unique.spice)

- The results obtaind are given [here](./Characterization%20Results.pdf)
- The plotted graph for threshold voltage (VTC), drain current (Id_max), gain (Av_max) and propogation delay (t_pd) is shown below

![graphs](images/Screenshot%202025-12-29%20225707.png)




    




