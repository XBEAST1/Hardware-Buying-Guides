# Universal Used PSU Safety & Inspection Guide

A practical, field-tested guide for evaluating used Power Supply Units (PSUs) without needing specialized lab tools or multimeter testing.

Designed for a strict **2-to-3 minute in-shop counter triage** using physical sensory inspection, chassis weight audit, and modular pinout verification to detect blown capacitors, melted wiring, fake safety certifications, and mismatched cable hazards before handing over payment.

---

## 🚫 1. Instant Dealbreakers (Walk Away Immediately)

If a used PSU triggers **ANY** of these 6 conditions at the shop counter, **reject it immediately**:

1. **Dangerous Tier-F / Known Exploding Models:**
   * Unit belongs to the confirmed hazardous failure list (e.g., **Gigabyte GP-P750GM / GP-P850GM** exploding batches, **Diablotek**, **Logisys**, **Aresgame**).
   * Catastrophic internal failure risks destroying connected motherboard, CPU, and graphics card components.
2. **Chemical, Ammonia, or Burnt Odor (The Sniff Test):**
   * *Fishy / rotten seafood smell:* Leaking or vented liquid electrolyte from degraded internal electrolytic capacitors.
   * *Burnt / acrid smell:* Overheated transformer magnetic windings or melted primary wire insulation.
3. **Punctured, Peeled, or Tampered Warranty Seals:**
   * Factory tamper-evident warranty sticker covering any chassis screw is pierced, slit, or missing.
   * Indicates unqualified amateur internal repair, DIY fan swapping, or blown fuse replacement.
4. **Bulging Capacitors or Loose Internal Debris:**
   * Cylindrical capacitors visible through the fan grill have domed, bulged tops or brown crusty electrolyte leakage.
   * Any metallic rattle of loose screws, solder blobs, or broken ferrites inside during the shake test (causes an instant dead short and spark).
5. **Missing, Mixed, or Third-Party Modular Cables:**
   * Seller supplies loose, mismatched, or third-party modular cables without verifiable pinout matching.
   * Modular backplane pinouts are **NOT standardized**. Mixing cables reverses 12V and Ground, instantly frying motherboards and storage drives.
6. **Missing 80 Plus Certification / Featherweight Generic Unit:**
   * Extremely lightweight (under 1.0 kg) grey tin casing with colorful, exaggerated wattage stickers and no verifiable safety certifications (UL, TÜV, CE).
   * Lacks active PFC, transient input filtering, and basic over-current/over-voltage protections.

---

## ⚡ 2. The 2-Minute Shop Field Test

When you pick up the power supply at the counter, execute this rapid sequence of physical and sensory checks before handing over payment:

```
[2-MINUTE COUNTER WORKFLOW]
The Sniff Test (20s) ──> The Shake Test (15s) ──> Weight Audit (15s) ──> Flashlight Cap Check (30s) ──> Modular Cable Audit (40s) ──> DECISION
```

### Step 1: The Sniff & Olfactory Check (20 Seconds, Cold or Unpowered)
Put your nose right against the honeycomb exhaust vent at the back and take a deep sniff. Any fishy, ammonia, or burnt-circuit odor confirms vented or dead capacitors. Walk away immediately.

### Step 2: The Physical Shake & Rattle Test (15 Seconds, Unpowered)
Gently tilt and rotate the PSU in your hands. Listen closely for loose screws, solder blobs, or broken plastic rattling inside. A loose conductive object inside will cause a catastrophic dead-short and spark the moment AC power is connected.

### Step 3: Chassis Weight & Component Mass Audit (15 Seconds, Physical Triage)
* A quality power supply feels **heavy and solid** (typically between 1.5 kg and 2.2 kg) because it has thick aluminum heatsinks, heavy copper magnetic transformers, and proper EMI filtering components.
* If an advertised "600W" PSU feels light like an empty tin can (under 1.0 kg), it is dangerous, low-grade hardware with stripped-down safety stages.

### Step 4: Flashlight Capacitor & Internal Inspection (30 Seconds, Visual Triage)
Shine your phone's flashlight through the cooling fan grill. Look at the round cylindrical capacitors on the circuit board: their metal tops must be **completely flat**. If any capacitor top is domed, bulged upward, or has brownish crust on it, the power supply is on the verge of death.

### Step 5: Modular Cable & Wire Gauge Verification (40 Seconds, Safety Check)
* **All-Black Flat Ribbon or Sleeved Cables:** The modern standard used by reputable gaming brands for more than 8 years. Indicates a modern platform with proper thick copper wiring (18 AWG or 16 AWG) safe for dedicated graphics cards.
* **Bare Multi-Colored Wires ("Ketchup & Mustard"):** Yellow, red, and orange bare wires indicate an ancient office PC pull from over 10 years ago or a bottom-tier generic Chinese budget unit. These frequently use dangerously thin copper wires (20–22 AWG) that can overheat, melt their plastic insulation, and catch fire or short out under modern gaming loads. Avoid pairing them with discrete gaming GPUs.

---

## 📊 3. Understanding 80 Plus: What Does It Actually Mean?

### What is 80 Plus?
The **80 Plus** badge is an **energy efficiency rating**, not a direct guarantee of build quality. It measures how much of the AC electricity drawn from your wall outlet actually gets converted into clean DC power for your PC components, and how much is wasted as **heat**:

* If your PC components draw **400W** under load:
  * An unrated 70% efficient generic PSU pulls **approximately 570W** from your wall (wasting 170W as pure heat into your room).
  * An **80 Plus Gold (90%)** PSU pulls **approximately 444W** from your wall (wasting only 44W as heat).

### The 80 Plus Tiers Explained: Simple vs. Bronze vs. Gold vs. Platinum

| Badge / Tier | Efficiency (at 50% Load) | What It Means in Real Life | Should You Buy It Used? |
| :--- | :---: | :--- | :--- |
| **80 Plus (White / Standard)** | **Approximately 80%** | The baseline entry tier. Generates more heat and higher electricity bills. Usually found in older budget office units. | **Only for ultra-budget / low-power PCs** (GPUs drawing under 75W). Avoid for modern gaming. |
| **80 Plus Bronze** | **Approximately 85%** | The popular budget sweet spot. Decent efficiency, affordable, and widely used in mid-range gaming builds. | **Great for budget gaming builds.** Just make sure it is from a reputable brand. |
| **80 Plus Silver** | **Approximately 88%** | Rare middle tier. Most manufacturers skip straight from Bronze to Gold because production costs are almost the same. | **Fine to buy**, but rarely found in the used market. |
| **80 Plus Gold** | **Approximately 90%** | **The Gold Standard.** High efficiency, runs cooler and quieter, uses higher-grade parts, and noticeably lowers electric bills. | **The Best Choice for Most Buyers.** Ideal for modern gaming GPUs (RTX 30/40, RX 6000/7000). |
| **80 Plus Platinum** | **Approximately 92%** | High-end enthusiast tier. Runs very cool and whisper quiet with premium internal components. | **Excellent**, but usually priced at a premium. |
| **80 Plus Titanium** | **94% or higher** | Flagship / Workstation tier. Maximum efficiency even at very low 10% idle loads. | **Top Tier**, but expensive and overkill for average gaming systems. |

### The Big 80 Plus Trap: Efficiency Does Not Equal Safety!
* **80 Plus only measures electricity savings. It does NOT test safety!**
* A power supply can achieve an 80 Plus Gold rating and still have terrible safety protections, cheap capacitors that fail after 2 years, or circuits that catch fire under load.
* *Real-World Example:* The infamous **Gigabyte GP-P750GM** that exploded under load on test benches was an officially certified **80 Plus Gold** power supply!
* **Takeaway:** Never buy a used PSU based *only* on a Gold sticker. Always check the brand reputation and tier list below.

---

## 🕵️ 4. Best PSU Brands & The Cultists Tier Guide

### Beware "Brand Blindness"
Never buy a power supply based *only* on the brand logo! Reputable companies like EVGA, Thermaltake, and Corsair sell **both top-tier legendary units AND dangerous budget units under the same brand name**. 

* An **EVGA SuperNOVA G2/G3** is a legendary, bulletproof Tier-A unit.
* An **EVGA W1 or N1** is an infamous fire-hazard that lacks basic temperature protections.
* A **Thermaltake Toughpower GF1/GF3** is an outstanding Tier-A power supply.
* A **Thermaltake Smart 80+ White** is an obsolete unit notorious for failing under gaming loads.

---

### The Master Brand & Model Buying Guide

| Brand | Top-Tier Flagship (Tier A)<br>*(RTX 3080/4080/4090, RX 7900)* | Mid-Range Sweet Spot (Tier B)<br>*(RTX 4060/4070, RX 6700/7700)* | Budget Safe (Tier C)<br>*(Low Power / under 150W GPU)* | Traps to AVOID (Tier E & F)<br>*(Fire Hazard / Unsafe)* |
| :--- | :--- | :--- | :--- | :--- |
| **Seasonic** | **Focus GX/PX (v3 / ATX 3.0)**, **Vertex**, **Prime TX/PX** | **Focus GX (v2)**, **Core GM/GX** | — | **S12II**, **S12III**, **M12II** *(outdated group-regulated designs)* |
| **Corsair** | **RMx (2021/2024 Shift)**, **HXi**, **SF750 / SF850 (SFX)** | **RMe Series (ATX 3.0)**, **CX / CX-M (2023)** | **CV650 / CV750** | **VS Series (orange label)**, **CV450/550**, older **Builder (green label)** |
| **Super Flower** | **Leadex III Gold**, **Leadex VII Gold/Plat (ATX 3.0)** | **Leadex V Pro**, **Leadex III Bronze** | — | Older Golden Green revisions |
| **be quiet!** | **Dark Power Pro 12/13**, **Straight Power 12** | **Pure Power 12M (ATX 3.0)**, **Pure Power 11 FM** | **System Power 9 / 10** | System Power U9 |
| **MSI** | **MPG A-GF (A750GF, A850GF)**, **MPG A-G PCIE5 (A850G, A1000G)** | **MAG A-GL Series (A650GL, A750GL, A850GL)** | **MAG A-BN (A550BN, A650BN)** *(Best entry budget unit)* | **MAG A-DN Series** *(missing protections)* |
| **ASUS** | **ROG Thor II**, **ROG Strix Gold Aura / v2** | **TUF Gaming Gold** | **TUF Gaming Bronze** | Older unrated TUF batches |
| **Cooler Master** | **V Gold V2**, **V Platinum**, **V SFX** | **MWE Gold V2 (Full Modular / ATX 3.0)** | **MWE Bronze V2** | **Elite Series (V3/V4)**, **MasterWatt Lite** |
| **EVGA** | **SuperNOVA G2 / G3 / P2 / T2 / G6** | **SuperNOVA GT / G5** | **EVGA BR (450–600W)** | **EVGA W1 / W2 / W3**, **EVGA N1**, **400B / BA / BV** |
| **Thermaltake** | **Toughpower GF1**, **Toughpower GF3 / GF3 ARGB** | **Toughpower GF A3**, **Smart BM2 / BM3** | — | **Smart 80+ White**, **Smart SE**, **Smart RGB**, **TR2 Series** |
| **XPG (ADATA)** | **Core Reactor / Core Reactor II (ATX 3.0)**, **Cybercore** | — | **XPG Pylon (450W–750W)** *(Top-tier budget Bronze)* | **XPG Probe** *(low-grade parts)* |
| **Cougar** | **Polar / Polar X2**, **GEX X2 (ATX 3.0)**, **GX-F** | **GEX (Gold)**, **BXM** | — | **VTE**, **VTC**, **STX**, **XTC** *(cheap group-regulated traps)* |

---

### Who Actually Makes Your PSU? (The True OEMs)
Most consumer brands don't own factories; they design the case and fan profile, then hire specialized manufacturers:
* **Seasonic & Super Flower:** Two of the only brands that build their own units in their own factories. They are the undisputed gold standard for reliability.
* **CWT (Channel Well Technology):** The high-performance manufacturer behind Corsair's **RMx**, MSI's **MPG/MAG**, Thermaltake's **Toughpower GF1/GF3**, and **XPG Core Reactor**.
* **Great Wall:** Elite engineering titan that builds Corsair's gold-standard **SF750** and ASUS **TUF Gaming Gold**.
* **FSP & HEC:** Veteran Taiwanese OEMs. FSP builds **be quiet!** Dark Power units and EVGA G5; HEC is the parent manufacturer behind **Cougar** and select be quiet! Pure Power units.

### Complete Blacklist (Dangerous Models & Brands)
If you see any of these in a used listing, **do not buy them under any circumstance**:
* **Gigabyte GP-P750GM & GP-P850GM** (explodes under load due to flawed over-power protection).
* **EVGA W1, W2, W3 & N1** (missing temperature protections, cheap boiling capacitors).
* **Thermaltake Smart 80+ White / Smart RGB** (poor voltage regulation, high failure rate).
* **Diablotek, Logisys, Apevia, Aresgame** (known fire hazards with fake wattage ratings).

---

## ⚠️ 5. The Modular Cable Rule: Pinout Verification

> [!WARNING]
> **Modular Cables are NOT Standardized Across Brands or Models!**
> While component-side plugs (motherboard, GPU, SATA) follow standard ATX specs, **PSU-side pinouts are completely proprietary**. 
> * **The Danger:** Mixing cables reverses polarity (e.g., routing +12V into ground or +5V lines), instantly vaporizing SSDs, hard drives, and motherboard chips upon power-on.
> * **The "Fit" Trap:** **A cable clicking into the PSU does NOT mean it is compatible!** Standard connector geometry allows rounded pins from completely incompatible cables to slide into square sockets with zero physical resistance.

---

### 30-Second Countertop Cable Audit

Perform these 4 quick visual checks on the cable bundle before handing over money:

1. **Connector Brand Stamps & Labeling:**
   * **Corsair:** Cables feature molded **"Type 3"** or **"Type 4"** stamps on the connector housing (or micro-sized **"Type 5"** on Shift/SFX units). Finding a "Type 4" cable in an EVGA or Seasonic box is an immediate red flag.
   * **EVGA:** Labels GPU cables as **"VGA"** (not "PCI-E") and CPU cables as **"CPU"**.
   * **Seasonic / ASUS:** Label component ends as **"PCI-E"** and **"CPU"**.
   * *Note on "PSU" stamp:* A stamp reading **"PSU"** is purely an *orientation marker* (showing which end plugs into the power supply). It does **not** mean it is compatible with other power supplies.
   * **Reject:** Mismatched fonts, blank generic plastic plugs mixed with branded ones, or conflicting brand markings across the bundle.

2. **Intra-Bundle Consistency Check:**
   * **Normal Factory Setup:** Reputable brands (Corsair RMx, Seasonic Focus Plus, EVGA G2) legitimately ship a round mesh-sleeved 24-pin cable (housing ripple capacitors) paired with flat-ribbon PCIe and SATA cables. This is standard factory configuration.
   * **The Real Red Flag:** Mismatch *within the same cable category* (e.g., one PCIe cable is flat ribbon while another is mesh-sleeved, or SATA cables have differing plastic gloss, clip shapes, or wire thicknesses). This proves the seller grabbed spare cables from a junk bin.

3. **PSU-Side Pin Split Check (Motherboard Header):**
   * If the PSU has a split motherboard port, the cable must match:
     * **Corsair Type 3/4:** Splits into a **10-pin + 14-pin** dual connector at the PSU end.
     * **Seasonic Focus/Prime:** Splits into an **18-pin + 10-pin** dual connector.
   * If the PSU backplane has split ports but the seller gives you a 1-piece 24-pin connector (or vice versa), the cable is **not original**.

4. **Essential Cable Inventory (The "Buy Online" Trap):**
   * Confirm the bundle includes the actual cables your PC needs:
     * **1x 24-pin ATX** (Motherboard)
     * **1x or 2x 8-pin EPS** (CPU, labeled "CPU")
     * **2x or 3x 8-pin PCIe** (GPU, labeled "PCI-E" or "VGA") or **1x 12V-2x6** (ATX 3.0)
     * **1x or 2x SATA cables** (Storage/Fans)
   * **The Trap:** Never accept a unit missing GPU or CPU cables on the premise of "buying a cheap replacement cable on AliExpress/Amazon." Generic cables online frequently carry reversed pinouts or thin wires (20–22 AWG), while verified custom sets (e.g., CableMod) cost \$30–\$50, wiping out all used-market savings.

---

## 📋 6. Fast Countertop Decision Matrix

| Test Passed? | Observation / Finding | Action |
| :---: | :--- | :--- |
| ✅ | Clean neutral odor, solid heavy chassis (between 1.5 kg and 2.2 kg), flat capacitor tops, Tier A/B/C model, verified original matching cables. | **BUY WITH CONFIDENCE** |
| ⚠️ | Minor cosmetic scratches on casing, but 100% passes sniff/shake test, flat capacitors, authentic cables, Tier B or C unit. | **NEGOTIATE DISCOUNT** |
| ❌ | Fishy, ammonia, or acrid burnt-circuit odor from exhaust vent. | **REJECT (Blown / Leaking Electrolyte)** |
| ❌ | Punctured, torn, or missing warranty screw seal. | **REJECT (Amateur DIY Internal Tampering)** |
| ❌ | Visible bulged/domed capacitors or loose screw/solder rattling inside. | **REJECT (Imminent Dead Short / Catastrophic Failure)** |
| ❌ | Missing essential cables or mixed/mismatched modular cables from other brands. | **REJECT (Fatal Reverse-Polarity Hazard)** |
| ❌ | Featherweight (under 1.0 kg) grey box, bare "ketchup & mustard" wires, or listed on Tier F blacklist. | **REJECT (Fire Hazard / No Protections)** |
| ❌ | Voltage drop exceeds 0.6V (12V rail drops below 11.40V under load), violating ATX 5% voltage regulation tolerance. | **REJECT (Defective Voltage Regulation)** |
