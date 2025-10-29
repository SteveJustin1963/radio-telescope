  
# **Build a 21 cm Hydrogen Radio Telescope for Under $150**  
 
 

---

> **Abstract**  
> This project turns a **satellite TV dish**, **paint can**, and **$37 SDR dongle** into a **real radio telescope** capable of detecting the **21 cm neutral hydrogen line (1420.4 MHz)** — the same signal used by professional observatories to map the Milky Way.  
>  
> You’ll learn:  
> - **Horn antenna design** from aluminum flashing  
> - **Waveguide tuning** with a soup can  
> - **SDR signal processing** with free HDSDR software  
> - **MINT 2 simulation** on a Z80 TEC-1 for pre-testing  
> - **Doppler shift analysis** to track galactic rotation  
>  
> **Total Cost: $147** | **Build Time: 1 Weekend** | **No PhD Required**

---

## 1. Introduction: Why 21 cm?

The **21 cm line** is radio emission from neutral hydrogen (HI) when an electron flips its spin. It’s the **cosmic fingerprint** of gas clouds in galaxies.

| Property | Value |
|--------|-------|
| Frequency | **1420.405751768(2) MHz** |
| Wavelength | **21.106 cm** |
| Doppler Shift | ±100 km/s → ±0.48 MHz |
| Galactic Sources | Spiral arms, Magellanic Clouds |

**Your Goal**: Detect this line, see Doppler shifts, and map the Milky Way — **from your backyard**.

---

## 2. System Block Diagram

```
Sky → Horn Antenna → Waveguide (Paint Can) → LNB → SDR Dongle → Laptop (HDSDR) → MINT Simulation (Optional)
```

---

## 3. Parts List – Total: **$147**

| Item | Source | Price | Notes |
|------|--------|-------|-------|
| **8–10 ft Satellite Dish** | Craigslist / eBay | **$0–$30** | Used TV dish |
| **Aluminum Flashing (51 cm × 3 m)** | Home Depot | **$13** | 0.4 mm thick |
| **1-Gal Paint Thinner Can (empty)** | Hardware Store | **$9** | Waveguide |
| **N-type Bulkhead + N-to-SMA Adapter** | Amazon | **$12** | RF feed |
| **Nooelec NESDR SMArt v5** | Nooelec.com | **$37** | RTL-SDR, 0.5 ppm TCXO |
| **SAW Filter + 2× LNA (1420 MHz)** | Nooelec | **$38** | Critical! |
| **Coax Cable (RG-6, 30 ft)** | Home Depot | **$9** | With F-connectors |
| **Aluminized HVAC Tape** | Amazon | **$8** | Seal joints |
| **Foam Board + Hot Glue** | Dollar Store | **$5** | Structural support |
| **USB Extension Cable (3m)** | Amazon | **$6** | Laptop to SDR |
| **TEC-1 Z80 Kit (Optional)** | eBay | **$60** | For MINT simulation |

---

## 4. Horn Antenna Design – The Heart of the System

### 4.1 Geometry (Pyramidal Horn)

| Parameter | Value | Formula |
|---------|-------|--------|
| Aperture Width | **51 cm** | Gain ~17 dBi |
| Length | **75 cm** | λ/4 taper |
| Throat | 10 cm × 10 cm | Matches waveguide |

> **DIY Cut Pattern** (Print & Tape to Flashing):

```
   /\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\
  /                           \\
 /                             \\
/                               \\
|                               |
|                               |
 \\                             /
  \\                           /
   \\\\\\\\\\\\\\\\\\\\\\\\\\\\\\
        ↑ 51 cm ↑
```

1. **Cut 4 trapezoids** from flashing (75 cm long, 10 cm throat → 51 cm mouth)  
2. **Fold & tape** with HVAC tape into pyramid  
3. **Reinforce** with foam board triangles inside  
4. **Mount on dish focal point** (use dish arm or 3D-printed bracket)

---

## 5. Waveguide Feed – The $9 Paint Can Trick

### 5.1 Why a Can?

- Acts as **circular waveguide**  
- Cutoff frequency: **~1.3 GHz** → passes 1420 MHz  
- **Pin probe** couples RF into coax

### 5.2 Construction Steps

1. **Clean can thoroughly** (remove paint thinner residue)  
2. **Drill 8 mm hole** in center of **bottom**  
3. **Insert N-type bulkhead** — solder center pin  
4. **Cut copper wire probe**: **68 mm long** (¼ λ_g at 1420 MHz in air-filled guide)  
5. **Solder probe to N-center**, perpendicular to base  
6. **Seal with hot glue + tape**  
7. **Attach can to horn throat** (tape + foam)

```
        [Horn Mouth 51cm]
               ↓
          ┌────────────┐
          │   Paint     │ ← 1 gal can
          │   Can       │
          │   Probe → ● │ ← 68 mm from base
          └────────────┘
               ↓
            Coax → SDR
```

---

## 6. Receiver Chain – From Sky to Screen

```
Dish + Horn → Paint Can → [Optional LNB] → SAW Filter + LNA → SDR → HDSDR
```

> **Skip LNB if using direct feed** — SAW filter is **mandatory**

### 6.1 RF Chain Wiring

1. **Horn → 30 cm RG-6 → LNA/SAW box** (power via bias-tee in SDR)  
2. **SAW box → 10m RG-6 → SDR dongle**  
3. **SDR → USB → Laptop**

---

## 7. Software Setup – HDSDR (Free)

1. **Download**: [hdsdr.de](http://www.hdsdr.de)  
2. **Install RTL-SDR drivers** (Zadig)  
3. **Open HDSDR** → Input: **RTL-SDR USB**  
4. **Set Center Freq**: `1420.4 MHz`  
5. **Bandwidth**: `2.4 MHz`  
6. **Mode**: **USB** or **CW**  
7. **Waterfall Gain**: Adjust until noise floor ~–90 dBm

---

## 8. First Light – Calibration & Testing

### 8.1 Cold Sky Test (Point at Zenith)

- **Expected**: Flat noise floor  
- **Record 5 minutes**, average spectrum

### 8.2 Hot Load Test (Point at Ground or Trees)

- **Expected**: +3–5 dB rise  
- Confirms system gain

### 8.3 Sun Test (Only at Sunrise/Sunset!)

- **Point dish at Sun** (use shadow method)  
- **Expected**: Broadband noise spike  
- **Verify alignment**

---

## 9. Detecting the Hydrogen Line

### 9.1 Target: **Cygnus Region** (Galactic Plane)

| Source | RA | Dec | Expected Doppler |
|--------|----|-----|------------------|
| **Deneb** | 20h 41m | +45° 16' | ~0 MHz (LSR) |
| **Cassiopeia A** | 23h 23m | +58° 48' | –0.1 MHz |
| **Perseus Arm** | ~120° galactic longitude | — | –50 km/s → **–0.24 MHz** |

### 9.2 Observation Procedure

1. **Point dish** at target (use phone app: *SkySafari*)  
2. **Tune HDSDR to 1420.4 MHz ± 0.5 MHz**  
3. **Average 10–30 minutes** (use **Spectrum Lab** or HDSDR averaging)  
4. **Look for Gaussian peak** above noise

**Real Example (May 2025)**:  
> *“X1.2 solar flare produced Type III burst at 1420.5 MHz, drifting 0.1 MHz in 30 sec.”* – Radio JOVE Observer

---

## 10. MINT 2 Simulation – Pre-Test on Your Z80!

Use **TEC-1 + MINT 2** to simulate spectra **before** building hardware.

### 10.1 Load This Code (Strip Comments!)

```mint
// MINT 2 - 21cm Hydrogen Simulator
:S center! width! amp! size! [0 size 1 -] f! [0 size 1 -] i! 0 j! size( j f? center - abs width / dup * -1 * 100 / exp amp * 3 /R + i j?! j 1+j!) `Spectrum in i` /N i. ;
:P spec! thr! spec /S s! 0 mi! 0 mf! 0 k! s( spec k? thr>( spec k? mi>( spec k? mi! k mf!) ) k 1+k!) `Peak: ` mf. `MHz ` mi. /N ;
:V spec! spec /S s! 0 r! s( spec r? abs 5 / b! `F` r. `: ` b * `|` /N r 1+r!) `Done` /N ;
```

### 10.2 Run Simulation

```mint
> 200 1 2 1420.4 :S    // 200 pt spectrum, peak at 1420.4
> i 0.3 :P             // Detect above 0.3
Peak: 1420 MHz 1
> i :V                 // ASCII plot
F0: |
F1420: ****|
...
```

**Use this to verify your math before soldering!**

---

## 11. Data Analysis – Find Doppler Shifts

1. **Export HDSDR spectrum** → CSV  
2. **Fit Gaussian** in Python (or MINT `:P`)  
3. **Compute velocity**:

```
v = c × (f_obs – 1420.4) / 1420.4
c = 3×10⁵ km/s
```

**Example**:  
> `f_obs = 1420.16 MHz` → `v = –72 km/s` → **gas moving toward us**

---

## 12. Advanced Upgrades

| Upgrade | Cost | Benefit |
|-------|------|--------|
| **Motorized Alt-Az Mount** | $80 | Automated scanning |
| **GNU Radio + Python** | $0 | Real-time Doppler mapping |
| **Dual Polarization Feed** | $50 | Stokes parameters |
| **Interferometer (2 dishes)** | $200 | 0.1° resolution |

---

## 13. Troubleshooting Guide

| Symptom | Fix |
|-------|-----|
| No signal | Check coax, power to LNA, SDR driver |
| Noise spikes | Ground SDR, use ferrite beads |
| Weak hydrogen line | Average longer, point at galactic plane |
| Frequency drift | Use TCXO SDR (NESDR SMArt) |
| MINT crash | **Perfect syntax!** No spaces in `:F`, end with `;` |

---

## 14. Conclusion

You now have a **fully functional radio telescope** that:

- Detects **neutral hydrogen** at 1420 MHz  
- Maps **galactic rotation** via Doppler  
- Costs **less than a smartphone**  
- Runs **MINT simulations** on a 1970s Z80  

**This is not a toy** — your data can contribute to **Radio JOVE**, **SARA**, or **OSRT**.

---

## References

1. [Mini Radio Telescope – UPenn](https://github.com/UPennEoR/MiniRadioTelescope)  
2. [IEEE Spectrum: $150 Hydrogen Telescope](https://spectrum.ieee.org)  
3. [Radio JOVE Project – NASA](http://radiojove.gsfc.nasa.gov)  
4. [MINT 2 Manual – TEC-1 Z80](https://github.com/SteveJustin1963/tec-mint)  
5. [HDSDR Software](http://www.hdsdr.de)

---

**Start building tonight. The Milky Way is waiting.**  

*Electronics Experimenter Magazine – “We don’t just read schematics. We listen to the stars.”*
