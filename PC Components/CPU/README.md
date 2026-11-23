# Universal Used CPU Inspection & Multi-Core Stability Guide

A fast, field-tested guide for evaluating used desktop processors (AMD Ryzen AM4/AM5 & Intel Core LGA 1200/1700).

Designed for a strict **3-minute in-shop counter triage** using physical optical inspection and portable diagnostic tools (CPU-Z, 7-Zip Benchmark, and Cinebench R23) to catch bent pins, arc-burned land pads, swapped counterfeit IHS lids, and degraded silicon (such as Intel 13th/14th Gen $V_{\text{min}}$ shifts) before handing over payment.

---

## 🚫 1. Instant Dealbreakers (Walk Away Immediately)

If the processor triggers **ANY** of these 6 conditions during inspection or testing, **reject it immediately**:

1. **Physical Pin & Pad Fatal Damage:**
   * **AMD AM4 (PGA):** Broken or missing memory channel or PCIe signal pins. (Losing even one signal pin causes total failure to POST or dead dual-channel memory).
   * **Intel LGA (1200/1700) & AMD AM5 (LGA):** Black or dark-charcoal **arc burn pitting** on the underside gold land pads, or deep mechanical gouges exposing bare copper/fiberglass. *(Note: Faint bluish/teal color or light pin dimples from normal socket pressure are completely harmless and NOT damage).*
2. **Missing or Fractured SMD Decoupling Capacitors (MLCCs):**
   * Missing, chipped, or cracked ceramic capacitors in the underside central cavity (Intel) or around perimeter cutouts (AMD AM5). Fractured MLCCs cause direct short circuits to ground (instant VRM trip) or uncorrectable WHEA parity errors.
3. **IHS Swapped Counterfeit Detection:**
   * CPU-Z displays fewer cores, fewer threads, or a lower **L3 Cache size** than the official specification (e.g., an advertised Core i9 showing only 4MB L3 cache or 4 cores confirms a cheap Celeron/Pentium with a swapped heat spreader).
   * The integrated heat spreader (IHS) has thick, squishy, bulging black RTV silicone seams and sealed breather vents.
4. **Decompression Failures or Arithmetic Aborts (Degraded Silicon):**
   * The **7-Zip Benchmark (32MB/64MB)** throws an immediate error (*"Benchmark canceled with errors"*) or silent crash during the **Decompressing** passes within 60 seconds.
5. **Instant BSOD / Core Lockup under AVX Load:**
   * Any Blue Screen of Death during Cinebench R23 or CPU-Z stress testing:
     * **`0x00000124` (`WHEA_UNCORRECTABLE_ERROR`)** $\rightarrow$ Hardware silicon failure / internal cache error.
     * **`0x00000101` (`CLOCK_WATCHDOG_TIMEOUT`)** $\rightarrow$ Core pipeline locked due to insufficient voltage.
6. **Thermal Collapse & 800 MHz Clock Lock:**
   * The CPU clock frequency craters to **800 MHz (0.79 GHz)** under load and package power drops below 35W (indicates severe PROCHOT thermal interrupt, broken internal thermal sensors, or severe socket contact failure).

---

## ⚡ 2. The 3-Minute Shop Field Test

Everything required for a rapid counter inspection is covered by three free portable Windows tools carried on a USB flash drive:
* **CPU-Z (Portable):** Hardware register verification, stepping, core topology, and L3 cache validation.
* **7-Zip (Portable):** 45-second decompression memory controller and ring-bus stability check.
* **Cinebench R23 (Portable):** 60-second AVX2 maximum current ($I_{\text{max}}$) and $V_{\text{droop}}$ stability test.

```
[3-MINUTE COUNTER WORKFLOW]
Optical Pin/Pad Inspection (45s) ──> CPU-Z Architecture Audit (30s) ──> 7-Zip Benchmark (45s) ──> Cinebench R23 1-Pass (1m) ──> DECISION
```

### Step 1: Optical Pin & Pad Pre-Check (45 Seconds, Power Off)
1. **For AMD AM4 Processors (PGA 1,331 Pins):**
   * Hold the processor at eye level and look down the pin rows and columns under direct light.
   * Verify optical coplanarity: All pins must form perfectly straight orthogonal lines.
   * *Pin Straightening Rule:* If 1–2 pins are slightly bent (under 30°), they can be gently realigned using an empty **0.5 mm lead-free mechanical pencil sleeve** or razor blade edge. However, acute 90° bends work-harden the copper alloy and will snap.
2. **For Intel LGA (1200/1700) & AMD AM5 (LGA 1718):**
   * Use your phone's flashlight at a **45° raking angle**.
   * Look closely at the gold land pads: Check for black circular arc-burn spots (caused by transient micro-arcing from bad socket pins).
   * **Normal Wear vs. Damage (The "Blue Haze" Rule):** 
     * **NORMAL (Safe to Buy):** Faint bluish, teal, or dull hazy patches on the gold pads. This is completely harmless. It is just the socket pins leaving tiny indentations that reflect ambient light off the blue PCB substrate, or minor surface patina from 1–3 years of normal heat.
     * **FATAL DAMAGE (Walk Away):** Distinct **charcoal black burn pits/craters** (electrical shorts) or deep scratches cutting through the gold down to pink copper.
   * Inspect the central cavity (Intel) or top perimeter (AM5) for sheared or cracked miniature ceramic capacitors.
3. **Motherboard Socket Inspection:**
   * Flash your light across the motherboard socket pins: A healthy socket produces a uniform holographic reflection. Any bent, twisted, or collapsed spring contacts will appear as dark voids or off-angle bright spots.

### Step 2: CPU-Z Architecture & Anti-Fraud Audit (30 Seconds)
1. Launch **CPU-Z** and inspect the main tab:
   * **Name & Specification:** Verify exact SKU string. Avoid engineering samples displaying generic labels (e.g., `Intel Core 0000`).
   * **Cores & Threads:** Must match official factory specs (e.g., Ryzen 7 7800X3D = 8 Cores / 16 Threads; Core i7-13700K = 8P + 8E / 24 Threads). Fewer cores indicate disabled/damaged cores.
   * **L3 Cache (The Ultimate Anti-Fraud Check):** An IHS lid swap cannot fake on-die hardware cache registers:
     * *Core i9-13900K / 14900K:* Must read **36 MB**.
     * *Core i7-13700K:* Must read **30 MB** (14700K reads **33 MB**).
     * *Ryzen 7 7800X3D:* Must read **96 MB** (32 MB base + 64 MB 3D V-Cache).
     * *Ryzen 7 5800X3D:* Must read **96 MB**.

### Step 3: The 7-Zip Decompression Rapid Check (45 Seconds)
*(This is the fastest test to expose degraded silicon and Intel 13th/14th Gen instability without waiting for full render passes).*

1. In 7-Zip, open the benchmark utility:
   $$\text{Tools} \longrightarrow \mathbf{\text{Benchmark}}$$
2. Set Dictionary Size to **`64 MB`** and select all available CPU threads.
3. Let it run for 2–3 full cycles (45 seconds) and watch the **Decompressing** column.
4. **Pass Criteria:** Must run smoothly without freezing.
   * *Instant Failure:* If the test throws an error (*"Error: Benchmark canceled with errors"*), displays corrupt hash values, or silently crashes to desktop, the silicon is degraded.

### Step 4: Cinebench R23 1-Pass AVX2 Stress (1 Minute)
1. In Cinebench R23, configure single-pass rendering:
   $$\text{File} \longrightarrow \text{Preferences} \longrightarrow \text{Minimum Test Duration: } \mathbf{\text{Off (0 minutes)}}$$
2. Click **CPU (Multi Core)** to run a single full render pass.
3. Open **HWiNFO64** in the background:
   * **Clocks:** Must sustain rated all-core boost clocks without plunging to 800 MHz.
   * **Core Temperature Delta:** Individual core temps should remain within **4°C to 8°C** of each other. A delta wider than 20°C across P-cores indicates mounting pressure or thermal paste failure.
4. **Pass Criteria:** The single pass must render completely without missing tiles, application crashes (`STATUS_ACCESS_VIOLATION 0xC0000005`), or system reboots.

---

## 📊 3. Master Hardware & Diagnostic Reference Table

| Socket / Family | Pin Architecture | Key Critical Inspection Area | L3 Cache Baseline | Common Used Trap |
| :--- | :--- | :--- | :--- | :--- |
| **AMD AM4** (Ryzen 1000–5000) | PGA 1,331 Pins | Gold pin straightness; check for snapped corner pins. | • 5600X: 32MB<br>• 5700X: 32MB<br>• 5800X3D: 96MB | Snapped memory bus pins causing loss of dual-channel RAM. |
| **AMD AM5** (Ryzen 7000–9000) | LGA 1,718 Lands | Top-side capacitor perimeter; look for chipped MLCCs. | • 7600X: 32MB<br>• 7700X: 32MB<br>• 7800X3D: 96MB | Thermal paste / conductive liquid metal spilled onto exposed capacitors. |
| **Intel LGA 1200** (10th/11th Gen) | LGA 1,200 Lands | Underside central MLCC cluster; gold contact pad wear. | • 10700K: 16MB<br>• 10900K: 20MB<br>• 11700K: 16MB | Missing cavity capacitors causing high-frequency Vcore ripple. |
| **Intel LGA 1700** (12th/13th/14th Gen) | LGA 1,700 Lands | Arc burn pitting on pads; substrate bending from socket latch. | • 12700K: 25MB<br>• 13700K: 30MB<br>• 14900K: 36MB | Vmin degradation / electromigration (13th/14th Gen instability). |

### Healthy Thermal Throttling vs. True Thermal Collapse

| Behavior | Healthy Thermal Throttling | True Thermal Collapse (Fatal Mounting / Sensor Fault) |
| :--- | :--- | :--- |
| **Clock Trajectory** | Smooth, modest step-down from peak boost to steady all-core boost (e.g., 5.4 GHz $\rightarrow$ 5.0 GHz). | Instant, cascading cliff dive down to emergency throttle states (**800 MHz / 0.79 GHz** lock). |
| **Temperature Curve** | Progressive climb over 15–30 seconds up to 90°C–95°C, stabilizing at a plateau. | Sub-second spike to 100°C–105°C in **under 3 seconds** of starting load. |
| **Package Power** | Sustained at or near rated PL1/TDP levels (e.g., 105W–180W). | Sharp power collapse from peak down to a trickle (**15W–35W**) to prevent die meltdown. |
| **Core-to-Core Delta** | Tight variance: $\Delta T$ across P-cores is **4°C to 8°C**. | Severe imbalance: $\Delta T$ exceeds **20°C to 35°C** across cores (tilted coldplate / dry pocket). |

---

## 🕵️ 4. Delidding Scams & Counterfeit IHS Fraud

### How the Scam Works
Fraudulent sellers take a budget processor (e.g., Celeron G6900 or Core i3-12100), delid it, remove the lid of a dead or broken Core i9-13900K/14900K, glue the high-end lid onto the cheap chip with black automotive silicone, and sell it at flagship prices.

### How to Spot It Instantly:
1. **Adhesive Seam Audit:**
   * **Factory OEM Seal:** Ultra-thin (0.1–0.2 mm), razor-uniform, hard black elastomer seal with dedicated breather notches.
   * **Counterfeit Relid:** Thick, rubbery, squishy black RTV silicone (thicker than 0.5 mm) with overflow smears and sealed breather vents.
2. **Capacitor Array Matching (Intel LGA 1700):**
   * Inspect the underside central cavity: A cheap Celeron has a sparse cluster of few capacitors. A Core i7 or i9 features a dense, highly populated array of capacitors.
3. **Dual-Serial Verification (FPO vs. ATPO):**
   * The **FPO (Batch #)** is laser-etched on the IHS.
   * The **ATPO (Serial #)** is encoded in a microscopic 2D Data Matrix barcode printed directly on the green PCB substrate corner.
   * Scan the substrate barcode with your smartphone camera: On a counterfeit swapped lid, the batch codes will not match or will register on Intel's warranty portal as a low-end chip.
4. **The Hardware Register Check:**
   * Check CPU-Z on boot: An IHS swap **cannot alter on-die cache or core counts**. If an "i9" shows 2 cores or 4MB L3 cache, it is a relidded scam.

---

## ⚠️ 5. Intel 13th & 14th Gen Raptor Lake Degradation

### The Root Cause & Symptoms
* **The Fault:** Elevated microcode voltage requests exceeding 1.55V–1.65V combined with uncapped motherboard BIOS defaults caused permanent electromigration in P-core and ring-bus interconnects, permanently shifting the minimum required voltage ($V_{\text{min}}$) upward.
* **The Used Market Danger:** Sellers often mask degradation by applying manual downclocks (-200MHz to -400MHz) or heavy positive voltage offsets in BIOS before selling.
* **The Symptoms:**
  1. **"Out of Video Memory" (OOM) Errors:** Occurs during DirectX 12 shader compilation in Unreal Engine games (Fortnite, Hogwarts Legacy, Remnant II). Oodle Kraken decompression runs on the CPU; degraded CPU bit-flips corrupt the shader stream, causing the GPU driver to throw a false "Out of Video Memory" error despite plenty of available VRAM.
  2. **7-Zip Decompression Errors:** Decompression passes fail within 30–60 seconds.
  3. **Frequent Game Crashes:** Silent crashes to desktop without error codes.

> [!TIP]
> **Countertop Rule:** Always **Clear CMOS** (reset BIOS to factory defaults) on the test bench before testing any used Intel 13th or 14th Gen Core i7 or i9 processor to strip away any hidden manual downclocks.

---

## 📋 6. Fast Countertop Decision Matrix

| Test Passed? | Observation / Finding | Action |
| :---: | :--- | :--- |
| ✅ | Straight pins / clean pads (faint blue/teal haze or socket pin dimples is normal), genuine CPU-Z specs & L3 cache, passes 7-Zip & Cinebench R23 with stable boost clocks. | **BUY WITH CONFIDENCE** |
| ⚠️ | 1–2 slightly bent AM4 pins (under 30°), passes optical alignment with pencil sleeve, passes all benchmarks after socketing. | **NEGOTIATE DISCOUNT** (Factor in repair risk). |
| ❌ | Broken/missing signal pins on AM4, or black arc-burn craters on LGA gold pads. | **REJECT (Hardware Damage)** |
| ❌ | Missing, cracked, or chipped SMD capacitors in central cavity / perimeter. | **REJECT (Electrical Fault)** |
| ❌ | L3 cache or core count in CPU-Z does not match official specification. | **REJECT (Swapped IHS Fraud)** |
| ❌ | 7-Zip benchmark throws error or crashes during decompression passes. | **REJECT (Degraded Silicon / $V_{\text{min}}$ Shift)** |
| ❌ | CPU-Z / Cinebench triggers WHEA BSOD `0x124`, clock lock at 800 MHz, or Core temp delta wider than 20°C. | **REJECT (Fatal Core Failure)** |

---

**Hardware Buying & Maintenance Guides**  
Authored by **M. Hamza** ([@XBEAST1](https://github.com/XBEAST1)). For the latest updates, companion component guides, and contributions, visit the [GitHub Repository](https://github.com/XBEAST1/Hardware-Buying-Guides).

