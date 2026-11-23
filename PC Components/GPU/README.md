# Universal Used GPU Inspection & Stress-Testing Guide

A fast, field-tested, and practical guide for evaluating used graphics cards (Nvidia GeForce GTX/RTX & AMD Radeon RX series).

Designed for a strict **10-to-15 minute in-shop counter triage** using portable diagnostic tools to detect failing VRAM, dying BGA solder joints, thermal paste pump-out, counterfeit VBIOS, and abusive crypto-mining wear before handing over payment.

---

## 🚫 1. Instant Dealbreakers (Walk Away Immediately)

If the GPU triggers **ANY** of these 6 conditions during inspection or testing, **reject it immediately**:

1. **Screen Artifacts & Texture Corruptions:**
   * Any purple/green dots, horizontal lines, checkerboard patterns, or flickering geometry during 2D desktop or 3D loads.
   * Indicates dying VRAM ICs or cracked BGA solder balls beneath the core.
2. **Instant Driver Crash / TDR Black Screen:**
   * Display freezes, driver crashes with a Timeout Detection and Recovery (TDR) error (`nvlddmkm.sys` or `amdkmdag.sys`), or PC instantly reboots the second a 3D stress test begins.
   * Confirms unstable core voltage delivery or microcode/memory channel breakdown.
3. **Severe Overheating or Massive Hotspot Delta:**
   * Hotspot temperature exceeds **105°C**, or hotspot gap wider than 25°C under load (more than 25°C above core temperature).
   * Indicates pump-out effect, dried out thermal paste, or warped heatsink coldplate.
4. **Driver Rejection or Hardware ID Mismatch:**
   * Official Nvidia/AMD Game Ready drivers refuse to install, or Windows Device Manager throws an error (**`Code 43`**).
   * GPU-Z displays mismatched specs, missing memory bus width, or fake VBIOS identifiers.
5. **Physical PCB Substrate Cracks:**
   * Any hairline fracture or copper delamination near the rear PCIe locking latch/notch.
   * On modern 12-to-15-layer PCBs, sag damage severs internal high-speed PCIe traces. This is **an unfixable fatal flaw**.
6. **Burnt Smell, Flux Residue, or Oven Reflow Clues:**
   * Sticky amber flux pooling around BGA chips, yellow/amber scorched underfill, or an acrid burnt plastic/silicon odor.
   * Proves previous amateur heat-gun/oven baking attempts to temporarily mask dying silicon.

---

## ⚡ 2. The 10-Minute Shop Field Test

Everything required for a rapid counter inspection is covered by free portable Windows utilities carried on a USB flash drive:
* **TechPowerUp GPU-Z (v2.12.0+):** Silicon identity, bus interface, and VBIOS authenticity.
* **HWiNFO64:** Real-time sensor monitoring (Core vs. Hotspot vs. Memory Junction, Fan RPM).
* **FurMark (Portable):** Quick 90-second Artifact Scanner.
* **Unigine Superposition (or 3DMark Time Spy):** Realistic 5-minute sustained 3D gaming load.

```
[10-MINUTE COUNTER WORKFLOW]
Physical & Smell Check (1m) ──> GPU-Z Verification (2m) ──> FurMark Artifact Scan (90s) ──> Superposition 4K (5m) ──> Fan Sweep (1m) ──> DECISION
```

### Step 1: Physical & Acoustic Pre-Check (1 Minute, Power Off)
1. **Sniff Test:** Smell the exhaust bracket and power headers. Any sweet burnt-varnish smell indicates failing components.
2. **PCIe Connector & Latch:**
   * Inspect the substrate latch notch for hairline cracks (common on heavy RTX 3080/3090/4090 GPUs shipped without support brackets).
   * Check the gold fingers for dull oxidation or grime (cleanable via the eraser technique in [Hardware Fixes & Cleaning Guide](../../Maintenance%20%26%20Troubleshooting/README.md#gpu--pcie-expansion-cards-gold-finger-cleaning)).
   * *The "Shorter Pin" Rule:* Pins **A1**, **B17**, **B31**, **B48**, and **B81** are factory-cut shorter by PCIe engineering specification for presence detection (`PRSNT2#`). **They are 100% normal and NOT broken pins**.
3. **Fans:** Spin fan blades manually with your finger. They should rotate smoothly and silently without wobbling, scraping the heatsink, or stopping abruptly.

### Step 2: GPU-Z Hardware Verification (2 Minutes)
1. Open **GPU-Z** and inspect the following fields:
   * **Name Banner:** Ensure there is NO red `[FAKE]` warning.
   * **Bus Interface:** Must show `PCIe x16 3.0/4.0 @ x16`. Click the **`?`** icon next to it to launch the mini-render test; verify that the link speed ramps up to full rated bandwidth (e.g., `@ x16 4.0`) rather than remaining stuck at `x1`, `x4`, or `x8`.
   * **Device ID & Shaders:** Cross-check the Device ID, Shader/CUDA core count, and memory bus width against the official TechPowerUp database.
   * **UEFI Checkbox:** The "UEFI" box in the bottom right corner must be checked.

### Step 3: FurMark Artifact Scanner (90 Seconds)
1. Open **FurMark** and check the box for **"Artifact Scanner"**.
2. Run at native screen resolution for 90 seconds while watching the artifact counter.
3. **Pass Criteria:** Artifact count must remain strictly **0**. If the counter ticks upward or yellow/green pixel flashes appear, VRAM memory cells are unstable.

### Step 4: Sustained Realistic 3D Load (5 Minutes)
*(Why not FurMark alone? FurMark triggers aggressive driver power limit clamping (`PerfCap: Pwr`), downclocking the core by 200–500 MHz below real gaming boost. A gaming benchmark tests true boost clocks and voltage stability).*

1. Launch **Unigine Superposition** (Preset: **4K Optimized** or **1080p Extreme**) or run a loop of **3DMark Time Spy**.
2. Open **HWiNFO64 (Sensors Only)** in the background and monitor during the test:
   * **Core Clock:** Confirm the card reaches and maintains its advertised boost clock.
   * **GPU Temperature (Main):** Must stay under **75°C–80°C**.
   * **GPU Hotspot:** Must stay under **90°C–95°C**.
   * **Hotspot Gap (Hotspot minus Main):** Should stay within **15°C to 20°C apart**.
   * **Memory (VRAM) Temperature:** Under **85°C** (or under **95°C** on high-power GDDR6X cards).
3. Listen for excessive high-pitched electrical screeching (severe coil whine) or fan rattling.

### Step 5: Fan Sweep & Bearing Check (1 Minute)
1. In **MSI Afterburner** or **FanControl**, disable "Auto" fan control.
2. **Low-Speed Test (Set Fan Speed Manually to 30%):** Set the fan speed slider manually to 30% and listen closely. Dry sleeve bearings will emit a rhythmic grinding, ticking, or scraping noise at low RPM that is usually masked at higher speeds.
3. **High-Speed Test (Set Fan Speed Manually to 100%):** Set the fan speed slider manually to 100% and let it run for 30 seconds. Verify in HWiNFO64 that all fan channels ramp up to their full speed (typically 2800–3500 RPM) and that no fan sensor drops to `0 RPM` (which indicates a tachometer sensor failure).

---

## 📊 3. Simple Temperature Guide

When testing the card under load (using Superposition or FurMark), check these numbers in HWiNFO64:

| Card Type | Normal Gaming Temp | Starts Getting Too Hot | Danger Zone (Walk Away) |
| :--- | :--- | :--- | :--- |
| **Nvidia (GTX & RTX)** | **Main:** 60°C–75°C<br>**Hotspot:** 70°C–85°C | **Main hits 83°C** or<br>**Hotspot hits 105°C** | **Main over 88°C** or<br>**Hotspot exceeds 105°C** |
| **AMD (Radeon RX)** | **Main:** 60°C–75°C<br>**Hotspot:** 75°C–90°C | **Main hits 90°C** or<br>**Hotspot hits 110°C** | **Main over 90°C** or<br>**Hotspot exceeds 110°C** |

### The "Hotspot Gap" (Quick Health Check)
In HWiNFO64, look at **GPU Temperature** (the main sensor) and **GPU Hotspot**. 

The Hotspot will always be warmer because it measures the single hottest point on the chip. Just check the gap between the two numbers:

* **Under 15°C gap (Great):** The cooler is making perfect contact and the thermal paste is fresh.
* **15°C to 20°C gap (Normal):** Typical for a card working hard under heavy gaming.
* **20°C to 25°C gap (Getting Dry):** The thermal paste is aging and drying out (the card still works fine, but plan to repaste it soon).
* **Hotspot gap wider than 25°C OR Hotspot exceeds 105°C (Walk Away):** The cooler is not touching the chip properly, or the thermal paste has completely dried and pumped out.

---

## 🕵️ 4. Heavy Wear & Crypto-Mining Checks

* **Amber / Yellowing PCB Halos (Excessive Heat):** Look at the backside of the PCB behind the VRAM chips. Cards that ran 24/7 under sustained heavy heat will show an amber, yellowish, or brown scorched tint on the green/black circuit board.
* **Silicone Oil Bleed vs. Liquid Metal:**
  * *Silicone Oil Bleed (Harmless):* Dark, damp-looking halos around thermal pads. This is normal non-conductive silicone oil sweating from thermal pads over time. It poses zero electrical danger and can be wiped clean with 90% or higher Isopropyl Alcohol.
  * *Liquid Metal Staining (Danger):* Silver-grey metallic crust or droplets. If someone applied liquid metal to an aluminum cooler, it causes **gallium embrittlement** (the metal crumbles like chalk). Any stray metallic droplet on surrounding tiny capacitors will cause an instant short circuit.
* **Repainted Memory Chips:** Some shady refurbishers spray matte black heat-resistant paint over heat-scorched memory chips and laser re-etch logos to disguise baked cards as factory fresh. Look closely for uneven paint texture or overspray around the chips.

---

## 🔍 5. Physical Inspection Checklist & Hardware Red Flags

| Component Area | What to Inspect | Acceptable Finding | Immediate Red Flag |
| :--- | :--- | :--- | :--- |
| **Warranty Screw Seal** | Sticker over spring-bracket retention screw | Broken seal is **acceptable IF** seller cleanly repasted and screws are intact. | Stripped screw heads, missing spring washers, chipped die corners from uneven pressure. |
| **PCIe Gold Fingers** | Edge connector contacts | Normal insertion scratches. Sense pins (A1, B17, B31, B48, B81) are factory-shortened. | Delaminated/peeled gold foil; deep gouges cutting through copper traces to raw fiberglass. |
| **Substrate Latch Notch** | Rear PCB retention hook | Clean, smooth fiberglass edge with no fractures. | **Hairline substrate crack** propagating into inner board layers. |
| **Heatsink Fin Stack** | Aluminum fin array | Light domestic dust that blows clear with air. | Dense white aluminum oxide crust or green copper patina (severe humidity/coastal corrosion). |
| **Heatpipes** | Sintered copper tubes | Clean copper or shiny nickel plating. | Deep black corrosion pitting or flattened/punctured heatpipe (vacuum loss). |

---

## 📋 6. Fast Countertop Decision Matrix

| Test Passed? | Observation / Finding | Action |
| :---: | :--- | :--- |
| ✅ | Clean PCB, genuine GPU-Z specs, Superposition stable, Hotspot gap under 15°C, quiet fans. | **BUY WITH CONFIDENCE** |
| ⚠️ | Hotspot gap between 20°C–25°C, high fan noise, genuine specs, zero artifacts. | **NEGOTIATE DISCOUNT** (Factor in cost of repasting with new thermal paste / pads). |
| ❌ | Official driver fails to install, or GPU-Z displays mismatched specs. | **REJECT / WALK AWAY** |
| ❌ | FurMark artifact scanner detects bit errors; screen displays colored dots or flashes. | **REJECT (Dying VRAM)** |
| ❌ | Hotspot gap wider than 25°C or Hotspot exceeds 105°C under load. | **REJECT (Overheating / Cooler Fault)** |
| ❌ | Hairline crack near PCIe notch, stripped screws, or sticky flux pooling around BGA chips. | **REJECT (Structural / BGA fault)** |

---

**Hardware Buying & Maintenance Guides**  
Authored by **M. Hamza** ([@XBEAST1](https://github.com/XBEAST1)). For the latest updates, companion component guides, and contributions, visit the [GitHub Repository](https://github.com/XBEAST1/Laptop-And-Mobile-Buying-Guides).

