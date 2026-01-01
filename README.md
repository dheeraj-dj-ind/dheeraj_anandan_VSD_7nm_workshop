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
- Standard cell area scaling in FinFET technologies refers to how the physical footprint of logic standard cells (like INV, NAND2, etc.) shrinks as the front‑end device geometries and cell architecture are scaled from node to node.
- Area can be decreased by modifying vertical (cell height) or horizaontal dimensions (cell width) 
- Fin depopulation is used to scale the cell height and also reduce capacitive load on standard cell inputs.
- Diffusion break prevents cross talk between transistors. 
![diff break](images/Screenshot%202025-12-26%20181417.png)
- Double Diffusion Break - Diffusion Break exists between two polysilicon or gate lines and cuts through active STI regions.
- Single Break - takes only one polysilicon and cuts through active region. 
- Contact Over Field Gate - Gate contact is placed directly on STI
- Contact Over Active Gate - Gate contact is either on active region or STI. This offers an inproved interconnection between cells and also reduces cell height

### 1.5.3 Parasitic Resistance
![para resistance](images/Screenshot%202025-12-26%20215628.png)
- Parasitic resistance is important in transistors.
- In planar transistors, the width of contact Wc is similar to width of channel Wg, where as in FinFETs, width of channel becomes smaller.
- In GAA, the channel length is even smaller because of stacking nature of device.
- In CFETs, extrinsic reistance is expected to by high.
![para resistance 2](images/Screenshot%202025-12-26%20215642.png)

### 1.5.4 Parasitic Capacitance
![para cap](images/Screenshot%202025-12-26%20220844.png)
- The gate capacitance decreases as you scale down technology and parasitic capacitance goes up upon scaling down.
- One way to minimize parasitic capacitence is by inserting a lower K material in the gap between gate and source-drain contact.
- Upon reducing K value, we get a lower effective capacitance. 

### 1.5.5 Device Scaling Using Layered Materials
![device scaling](images/Screenshot%202025-12-27%20092025.png)
- We can use layered materials to modify the gate lenghts to 5nm. 
- The main challenge faced in transistors is direct source to drain tunnelling, which prevents gate length scaling to short channels.
- 2D materials can be deposited with atomic scale precision. For eg. a layer of MoS2 is about 0.65nm thich and can be placed on a wafer with precision. 
- Channel thickness is a significant contributor to variability in transistors
- 2D materials have a slighlty higher effective mass compared to silicon. The source to drain tunnelling can be reduced by increasing effective mass of carriers.

### 1.5.5 Transistor Scaling to Sub 5nm Gate Lenghts
![sub 5nm](images/Screenshot%202025-12-27%20092900.png)
- Ideally, charge leakage should be outside the channel, but it is observed both outside as well as inside the channel, which is a major problem in short channel transistors.
- Upon scaling, problems such as low inplane dielectric constant arises. In order to fix this, the drain terminal cpacitnce should be lower than oxide capacitance.

### 1.5.6 MoS Transistor with 1nm Gate Length
![MoS 1nm](images/Screenshot%202025-12-27%20094118.png)
- Transistors are made of MoS2 channel and 1nm, single walled carbon nanotube gate. 
- The gate oxide is made up of ZrO2 (Zirconium Di-Oxide).
- Such transistors have a on/off current ratio of approximately 10^6 and a near sub threshold swing of 65 mV/decade.

### 1.5.7 All 2-D MOSFET
![2D mosfet](images/Screenshot%202025-12-27%20094624.png)
- 2D materials are atomically thin, precise and have no dangling bonds.

- Electrical Characteristics of all 2D FET
    - Excellent on/off current ratio.
    - Good output characteristics.
    - Constant mobility with gate electric field - scattering of electrons is less due to less surface roughness. 
    - The mobility does not degrade at high electric fields, allows for high drive current adn also Vdd scaling.

### 1.5.8 Body-Bias Effect
![TMDs](images/Screenshot%202025-12-27%20101148.png)
- In planar transistors, the threshold voltage (Vt) can be changed due to body effect.
- However. in FinFETs applying body effect is quite challenging. But by forming a fin by placing oxide between channel material and body, Vt scaling can be performed.
- Along with that, channel potential can also be modified.
- By modifying the oxide thickness, Vt can be changed by several 100vm with about 2V change in body voltage

### 1.5.9 Transistor Level Monolithics
![monolithics](images/Screenshot%202025-12-27%20101318.png)
- Monolithic 3D two layer CMOS have N and P transistors placed on top of each other. thereby reducing the area upto 50%
![Area saving graph](images/Screenshot%202025-12-27%20101620.png)
![Monolithics ckt](images/Screenshot%202025-12-27%20101629.png)
- For an inverter, the gain has to be greater than 1 to operate. From the graph, Gain = 1 at 150mV, which shows that device operates at low supply voltage.

### 1.5.10 Interconnects 
![interconnects](images/Screenshot%202025-12-27%20111214.png)
- Dual Damascene Copper interconnects are successors of Al interconnects due to their high resistance
- As technology shrinks down, the hole becomes narrower so we go to a single damascene process where via and metal are filled separatley.
- We can replace Cu with other metals that require no barrier or thinner barriers.
- Metals like Rutherium have low resistance, low feature size and do not require thick barriers.
![cu interconnects](images/Screenshot%202025-12-27%20112215.png)
- Extended Cu interconnects are used as there is high resistance in normal interconnects due to barriers
- Removing the top plate barrier, allows via resistance to reduce by 50%.

### 1.5.11 Backside Power Distribution Network
![back pdn](images/Screenshot%202025-12-27%20114138.png)

- If we choose a front side power delivery metwork, it has to go through almost 17 interconnect layers. Also there are more routing tracks for power and ground delivery to transistors.
- A better solution is to supply power from backside, as vias have larger resistance and thus signal takes time to reach the destination. 
- Backside Power Delivery Method can also help in reducing the standard cell area without losing signal tracks. 



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

- Inverter Schematic

![inv sch](images/Screenshot%20from%202025-12-31%2010-15-58.png)

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

## 2.3 Assignment with Unique Voltage
The uniquie voltage Vunique is given by ASCII{dheeraj}={100+104+101+101+114+97+107} = `0.723 V` 

The assignment given was to find characteristics of an inverter over a range of number of fins for both NMOS and PMOS in a inverter circuit. By using a loop, an excel spread sheet is created varrying Nfin_N and Pfin_N from 7 to 21, with a unique voltage `Vuniq`. The spice code is given below

- [SPICE Deck](attachments/inverter_vtc_unique.spice)

- The results obtaind are given [here](./Characterization%20Results.pdf)
- The plotted graph for threshold voltage (VTC), drain current (Id_max), gain (Av_max) and propogation delay (t_pd) is shown below

![graphs](images/Screenshot%202025-12-29%20225707.png)

# 3. Bandgap Reference Circuit
A Bandgap Reference Circuit is a voltage source that supplies a stable voltage proportional to the bandgap energy of semiconductor devices. They are nearly independent of temperature, supply voltage and process variations. In the below reference ckt, there are two bracnhes - `Startup and Reference Branch`, which helps in balancing ckt overall. From the `Reference` branch we calculate Vref and VCTAT.
In order to create a BJT in Xschematic, we use NFETs that have their drain and gate terminals connected.

![bandgap](images/Screenshot%202025-12-31%20093448.png)

## 3.1 Application of Bandgap Circuits
- LDO Regulators – Provides precise reference voltage for feedback loop; essential for on-chip power management in SoCs.
- ADC/DAC References – Stable V_REF for SAR, Sigma-Delta converters; directly impacts ENOB (effective number of bits).
- PLL/VCO Bias Circuits – Generates stable control voltages for charge pumps, VCO tuning; critical for clock generation.

## 3.2 Schematic of Bandgap Circuit
![bandgap](images/Screenshot%20from%202025-12-31%2012-44-41.png)

- NgSpice Console Output
![ngspice](images/Screenshot%20from%202025-12-31%2013-53-13.png)

The spice file for this circuit is given [here](/bandgap/bangap_ref.spice)

### Graphs obtained 

- VCTAT

![vctat](images/Screenshot%20from%202025-12-31%2012-44-51.png)

- Vref - VCTAT

![vref - vctat](images/Screenshot%20from%202025-12-31%2012-45-00.png)

- Vref

![vref](images/Screenshot%20from%202025-12-31%2012-45-13.png)

- Temperature Coefficient 

![temp_coef](images/Screenshot%20from%202025-12-31%2012-45-17.png)

## Assignment with Unique Resistance 
The uniquie resistance R3 is given by ASCII{dheeraj}={100+104+101+101+114+97+107} = `723 ohms`

### DC Analysis
The spice code for this is given [here](/bandgap/bandgap_dc_sim.spice)

![Schematic](images/Screenshot%20from%202025-12-31%2013-53-35.png)

#### Output Obtained

- NgSpice Window Output

![Ngspice](images/Screenshot%20from%202025-12-31%2013-53-13.png)

- dvref_dt

![dvref_dt](images/Screenshot%20from%202025-12-31%2012-45-17.png)

- Vref

![vref](images/Screenshot%20from%202025-12-31%2013-53-20.png)

- VCTAT

![vctat](images/Screenshot%20from%202025-12-31%2013-53-23.png)

- VPTAT

![vptat](images/Screenshot%20from%202025-12-31%2013-53-25.png)

### Transient Analysis

The spice file for the transient analysis is [here](/bandgap/bangap_trans.spice)

#### Observed Output

- Spice console 

![spice](images/Screenshot%20from%202025-12-31%2014-23-25.png)

- VPTAT

![VPTAT](images/Screenshot%20from%202025-12-31%2014-17-36.png)

- VCTAT

![VCTAT](images/Screenshot%20from%202025-12-31%2014-17-33.png)

- Vref 

![Vref](images/Screenshot%20from%202025-12-31%2014-17-24.png)

### Characterization Table

|S.No.|Vdd (V)|Temp °C |Vref(mv)|Line Regulation (mv/V)|Startup Time|
|  1. | 0.8   |   27   |  143.9 |     2.056337e+02     |            
|  2. | 0.9   |   27   |  158.9 |     2.270246e+02     |
|  3. | 1.0   |   27   |  101.2 |     2.525744e+02     |
|  4. | 1.0   |  -40   |  416.1 |     2.434650e+02     |
|  5. | 1.0   |  125   |  219.0 |     2.79293-e+=2     |

- Temperature Sweep
Using the below SPICE code, we print the Vref from -40°C to 125°C in steps of 1 
```bash
.dc temp -40 125 1
.control
run
print Vref
```

Line regulation is the ability of a power supply or voltage regulator to maintain a constant output voltage despite variations in the input (supply) voltage, with constant output load current.

- SPICE Code to Print Line Regulation

```bash
meas DC Vref_Max MAX v(Vref)
meas DC Vref_Min MIN v(Vref)
let line_regulation = (Vref_Max - Vref_Min)/0.7*1000
print line_regulation
```

For the Bandgap Reference Circuit, we can varry the supply voltage from 0.7v to 1.4v

# Acknowledgements and References 
Kunal Gosh [LinkedIn](https://www.linkedin.com/in/kunal-ghosh-vlsisystemdesign-com-28084836/)
Soundarya Madhuri Royyuru [LinkedIn](https://www.linkedin.com/in/royyurumadhuri/)
[Reference Repositary](https://github.com/arunkpv/vsd_asap7_workshop/blob/main/README.md)
[Reference Repositary](https://github.com/RSMadhuri66/Bandgap-Reference-Circuit-with-SCMB-with-ASAP-7nm-PDK-)





    




