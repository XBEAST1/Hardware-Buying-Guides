# Universal Used SSD Health, TBW & Anti-Counterfeit Guide

A fast, field-tested guide for evaluating used Solid State Drives. Covers both **M.2 NVMe PCIe SSDs** (PCIe 3.0, 4.0, and 5.0) and **2.5" SATA III SSDs** (250GB to 8TB+).

Designed for a strict **3 to 5 minute in-shop counter triage** using portable diagnostic utilities to detect uncorrectable flash memory degradation, fake controller firmware, hollow microSD scams, and cyclic overwrite capacity fraud before handing over payment.

---

## 🚫 1. Instant Dealbreakers (Walk Away Immediately)

If the SSD triggers any of the conditions in its category during counter inspection, **reject it immediately**:

### Category A: M.2 NVMe PCIe SSD Dealbreakers
1. **Critical CrystalDiskInfo Health Warnings:**
   * CrystalDiskInfo reports **Caution** (yellow) or **Bad** (red).
   * S.M.A.R.T. health percentage sits below **70%** (indicates severe prior host write exhaustion).
2. **Critical NVMe S.M.A.R.T. Errors (Raw Value MUST be strictly 0):**
   * **`01` Critical Warning (Must be 0):** Any non-zero count indicates available spare blocks exhausted, temperature trip, unrecoverable reliability loss, or write-locked read-only mode.
   * **`0E` Media and Data Integrity Errors (Must be 0):** Permanent uncorrectable ECC errors, flash memory corruption, or silent bit rot. Any count of 1 or higher confirms an immediate fatal failure.
   * **`03` Available Spare (Must be 90% or higher):** Healthy drives report 100%. If available spare drops below 90%, the drive is actively burning through its backup flash cells (trips Critical Warning if it reaches OEM threshold `04`).
3. **Severed PCIe Data Lanes / Interface Negotiation Drops:**
   * Drive negotiates at `PCIe 3.0 x1` or `PCIe 4.0 x2` instead of full rated bandwidth (e.g. `PCIe 4.0 x4` or `PCIe 3.0 x4`).
   * Indicates cracked solder joints beneath the controller, sheared SMD capacitors, or oxidized M.2 gold pins.
4. **Counterfeit Controller or Spoofed Identity:**
   * A Samsung drive (e.g., 980 Pro or 990 Pro) fails authentication in **Samsung Magician** (reports *"Genuine: False"*, *"N/A"*, or displays an unrecognized volume).
   * Controller lacks a metallic nickel heat spreader and uses budget third-party silicon (Maxio MAP1602, Realtek RTS5765DL, SMI SM2263XT) under a counterfeit label.
5. **Real-Time Post-Stress Increment:**
   * Running a quick 1 GiB write test causes **`0E`** (Media Errors) or **`0F`** (Error Information Log Entries) to increment in real time during testing.
6. **Catastrophic Write Freezes (0 MB/s Stutters):**
   * Write speed collapses and completely freezes at **0 MB/s for 3 to 10+ seconds** during basic file transfers (indicates the controller is locked in emergency voltage-shifting read-retry loops).

### Category B: 2.5" SATA III SSD Dealbreakers
1. **Critical CrystalDiskInfo Health Warnings:**
   * CrystalDiskInfo reports **Caution** (yellow) or **Bad** (red).
   * S.M.A.R.T. health percentage sits below **70%** for an everyday boot drive (driven by `B1` Wear Leveling Count on Samsung, or `E7` SSD Life Left on Crucial and Kingston).
2. **Critical SATA S.M.A.R.T. Errors (Raw Value MUST be strictly 0):**
   *(Note on Brands: SATA SSD S.M.A.R.T. attributes vary by manufacturer. Crucial, Kingston, and WD use `05`, `C5`, and `E7`. Samsung uses `B1`, `B3`, `B7`, `B5`, and `B6`. Check the attributes present on your specific drive).*
   * **`05` Reallocated Sectors / `B7` Runtime Bad Blocks (Must be 0):**
     * Crucial, WD, and Kingston report **`05`**. Samsung drives report **`B7`** (Runtime Bad Blocks) or **`05`**.
     * Any count of 1 or higher confirms permanent physical flash block retirement.
   * **`B5` Program Fail Count & `B6` Erase Fail Count (Must be 0):**
     * Present on Samsung and SanDisk drives. Any count of 1 or higher indicates flash memory cells failing under write or erase voltage.
   * **`B3` Used Reserved Blocks (Must be 0) / `B4` Unused Reserved Blocks (Must stay high):**
     * Samsung drives report **`B3`** (spare blocks consumed, which must be 0) and **`B4`** (remaining reserve pool). Crucial and Kingston report **`B4`**. If `B3` rises above 0 or `B4` drops to 0, factory backup flash is depleted.
   * **`BB` Reported Uncorrectable (Must be 0):**
     * Read errors that could not be recovered by hardware ECC. Present across all brands *(Warning: Drive can show a blue "Good" badge even with BB of 1 or higher!).*
   * **`C5` Current Pending Sectors (Must be 0):**
     * Present on Crucial, WD, and Kingston (frequently omitted on Samsung). Any count of 1 or higher indicates unstable flash blocks awaiting retirement.
   * **`C7` UltraDMA CRC Error Count (Must be 0 or stable):**
     * Universal across all SATA brands (labeled "CRC Error Count" on Samsung). Non-zero indicates damaged SATA data cables or dirty connector pins. Reject if count increases during testing.
   * **`E7` SSD Life Left / `B1` Wear Leveling Count (Must be 10% or higher):**
     * Crucial and Kingston report **`E7`**. Samsung reports **`B1` Wear Leveling Count** (the Current score of B1 directly sets the drive health percentage). Reject if health drops below 70% for a boot drive.
3. **Hollow Shell / MicroSD Array Scam:**
   * Drive weighs under **30 grams** (authentic metal/ABS encased SSDs weigh **40g–60g**).
   * Drive produces a resonant, hollow plastic sound when tapped, indicating an empty shell housing a cheap microSD card glued to an internal adapter.
4. **SATA Interface Transfer Mode Degradation:**
   * Drive reports **SATA/300** or **SATA/150** instead of **SATA/600** (SATA III 6 Gbps) when connected to a confirmed SATA III dock or motherboard port.
5. **Real-Time Post-Stress Increment:**
   * Running a quick 1 GiB write test causes **`05`**, **`B7`**, or **`C5`** to increment in real time.
6. **Severe Write Collapse on Sustained Transfers:**
   * Sequential write throughput drops below **20 MB/s** or freezes during a basic 1 GiB test pass (indicates worn-out DRAM-less QLC or fake flash).

---

## ⚡ 2. The Shop Field-Testing Sequence

Everything required for a rapid counter inspection is covered by three free portable Windows utilities carried on a USB flash drive:
* **CrystalDiskInfo (Portable):** Health audit, raw decimal telemetry, interface link verification.
* **CrystalDiskMark (Portable):** Quick 1-pass bus throughput and controller channel check.
* **ValiDrive / Manufacturer Tool (Samsung Magician):** Cryptographic authenticity and true LBA memory verification.

---

### Part A: M.2 NVMe SSD Field Test (3 Minutes)

```
[M.2 NVMe COUNTER WORKFLOW]
Physical & Controller Check (30s) ──> CDI Decimal & PCIe Link Audit (1m) ──> 1-Pass CDM Burst (30s) ──> NVMe SMART Delta Check (30s) ──> DECISION
```

#### Step 1: Physical & Controller Inspection (30 Seconds, Power Off)
1. **Controller Inspection:** Gently check the controller chip beneath the label edge:
   * Genuine high-end Samsung drives (970 EVO Plus, 980 Pro, 990 Pro) feature a shiny **nickel-plated metallic silver controller cap**. Counterfeit drives use cheap matte-black epoxy resin chips (Maxio or Realtek).
2. **Dedicated DRAM Verification:**
   * Inspect the PCB for a dedicated onboard DRAM cache chip (e.g., Samsung LPDDR4). If solder pads for DRAM are empty, the drive is a budget DRAM-less model or a counterfeit.
3. **Gold Pin Inspection:**
   * Inspect the M.2 M-key edge connector for scratched gold fingers, chips, or dark arc burns.

#### Step 2: CrystalDiskInfo Decimal Audit (1 Minute)
1. Open **CrystalDiskInfo** with Administrator privileges.
2. **Crucial Setup Step:** Switch Raw values to decimal:
   $$\text{Function} \longrightarrow \text{Advanced Feature} \longrightarrow \text{Raw Values} \longrightarrow \mathbf{10\text{ [DEC]}}$$
   *(Default Hexadecimal disguises severe errors: raw hex `0x0000000A` looks minor but represents 10 uncorrectable bad blocks!).*
3. **Verify PCIe Link Width:**
   * Ensure **Transfer Mode** matches official specifications (e.g., `PCIe 4.0 x4 | PCIe 4.0 x4`).
   * If it negotiates at `PCIe 3.0 x1` or `PCIe 4.0 x2`, clean the M.2 slot or reject the drive for severed data traces.
4. **Audit Critical NVMe Telemetry:**
   * Confirm **`0E` (Media Errors)** = **0**.
   * Confirm **`01` (Critical Warning)** = **0**.
   * Confirm **`03` (Available Spare)** is **90% or higher**.
   * Note the baseline value of **Total Host Writes (`07`)**.

#### Step 3: CrystalDiskMark Targeted 1-Pass Burst (30 Seconds)
*(Never run default 5-pass / All-row benchmarks on used SSDs at a shop. It writes 20–40 GB, overheats uncooled drives, and wastes time).*

1. Set Test Size: **`1 GiB`**.
2. Set Passes: **`1`** (change `5` to `1`).
3. Click ONLY the top **`[SEQ1M Q8T1]`** button:
   * **PCIe Gen 5 (Crucial T700, Next-Gen):** Expect **10,000–14,000 MB/s**.
   * **PCIe Gen 4 (Samsung 980 Pro, WD SN850X):** Expect **5,000–7,000 MB/s**.
   * **PCIe Gen 3 (Samsung 970 EVO, Crucial P3):** Expect **2,500–3,500 MB/s**.
   * *Trap:* If a "Gen 4" drive caps out at 2,000 MB/s or writes at 30 MB/s, it is a counterfeit or degraded drive.

#### Step 4: Post-Stress NVMe Delta Refresh (30 Seconds)
1. In CrystalDiskInfo, press **`F5`** (Refresh).
2. **The Verification:**
   * If NVMe `0E` (Media Errors) increased by **1 or more** $\implies$ **Reject drive (active flash cell degradation)**.
   * If NVMe `0F` incremented $\implies$ **PCIe bus communication errors (dirty gold contacts or damaged lanes)**.

---

### Part B: 2.5" SATA III SSD Field Test (2 Minutes)

```
[2.5" SATA COUNTER WORKFLOW]
Weight & Tap Check (20s) ──> CDI Decimal & SATA Link Audit (40s) ──> 1-Pass CDM Burst (30s) ──> SATA SMART Delta Check (30s) ──> DECISION
```

#### Step 1: Physical Weight & Casing Integrity Check (20 Seconds, Power Off)
1. **The Weight Test:**
   * Hold the drive in your hand. Authentic 2.5" SATA SSDs feel solid and weigh **40g–60g**.
   * If the drive feels featherlight like an empty plastic shell (under 30g), it is a counterfeit housing a glued microSD card.
2. **The Tap Test:**
   * Tap the casing center with a fingernail. Authentic drives produce a dull, dense thud. Hollow fakes produce a resonant plastic click.
3. **Connector Pin Check:**
   * Inspect the 7-pin SATA data and 15-pin power contacts for oxidation, bent pins, or cracked L-shaped plastic keys.

#### Step 2: CrystalDiskInfo Decimal Audit (40 Seconds)
1. Open **CrystalDiskInfo** with Administrator privileges.
2. **Crucial Setup Step:** Switch Raw values to decimal:
   $$\text{Function} \longrightarrow \text{Advanced Feature} \longrightarrow \text{Raw Values} \longrightarrow \mathbf{10\text{ [DEC]}}$$
3. **Verify Transfer Mode:**
   * Must read **SATA/600 | SATA/600** (SATA III 6 Gbps).
   * If it reports SATA/300, verify whether the shop's dock or cable is SATA II before proceeding.
4. **Audit Critical SATA Telemetry:**
   * **Overall Health:** Check the Health Status badge (driven by `B1` Wear Leveling Count on Samsung, or `E7` on Crucial and Kingston). Must be **80% or higher** (reject if below 70%).
   * **Bad Flash Blocks:** Confirm **`05` (Reallocated Sectors)** or **`B7` (Runtime Bad Blocks)** = **0**.
   * **Spare Block Reserve:** Confirm **`B3` (Used Reserved Blocks)** = **0** and **`B4` (Unused Reserved Blocks)** remains high.
   * **Program and Erase Integrity:** Confirm **`B5` (Program Fail)** = **0** and **`B6` (Erase Fail)** = **0**.
   * **Read ECC Errors:** Confirm **`BB` (Reported Uncorrectable)** = **0**.
   * **SATA Cable and Connection:** Confirm **`C7` (UltraDMA CRC Errors)** = **0** (or stable without incrementing).

#### Step 3: CrystalDiskMark Targeted 1-Pass Burst (30 Seconds)
1. Set Test Size: **`1 GiB`**.
2. Set Passes: **`1`** (change `5` to `1`).
3. Click ONLY the top **`[SEQ1M Q8T1]`** button:
   * **SATA III Standard (Crucial MX500, Samsung 870 EVO, WD Blue):**
     * Sequential Read: **500–550 MB/s**.
     * Sequential Write: **450–520 MB/s**.
   * *Trap:* If write speed crawls at **5–20 MB/s**, it is a counterfeit microSD fake or a severely degraded DRAM-less drive.

#### Step 4: Post-Stress SATA Delta Refresh (30 Seconds)
1. In CrystalDiskInfo, press **`F5`** (Refresh).
2. **The Verification:**
   * If SATA `05`, `B7`, `B3`, `B5`, `B6`, or `C5` incremented $\implies$ **Reject drive (active physical flash failure under stress)**.
   * If SATA `C7` incremented $\implies$ **SATA bus transmission fault (clean pins using eraser or replace cable)**.

---

## 📊 3. Master S.M.A.R.T. Reference Tables

### Subsection 3A: M.2 NVMe SSD Telemetry (CrystalDiskInfo)

| ID (Hex) | Attribute Name | Target Raw (10 [DEC]) | Assessment Standard & Action |
| :---: | :--- | :---: | :--- |
| **`01`** | **Critical Warning** | **0** | **Must be strictly 0.** Non-zero indicates spare block exhaustion, overheating, or read-only mode. |
| **`03`** | **Available Spare** | **90% or higher** | Percentage of factory reserve blocks remaining. Healthy drives report 100%. If available spare drops below 90%, the drive is actively retiring bad NAND. |
| **`04`** | Available Spare Threshold | Roughly 10% | Manufacturer minimum safety floor. If `03` falls below `04`, Critical Warning Bit 0 trips. |
| **`05`** | **Percentage Used** | **Below 30%–50%** | Mathematical odometer: $\text{Health \%} = 100 - \text{Percentage Used}$. *(Warning: Can show 99% health while actively dying if host writes were low!).* |
| **`07`** | **Data Units Written** | Variable | 1 Unit = 500 KB. Calculate true TBW: $(\text{Raw} \times 512,000) / 10^{12} = \text{TB Written}$. |
| **`0E`** | **Media and Data Integrity Errors** | **STRICTLY 0** | **FATAL RED LINE.** Any count of 1 or higher confirms uncorrectable ECC errors and silent bit rot. **REJECT.** |
| **`0F`** | **Error Information Log Entries** | **0** | Lifetime PCIe protocol errors. If 0F is 1 or higher while 0E is 0, inspect M.2 pin contacts for dust or damage. |

### Subsection 3B: 2.5" SATA III SSD Telemetry (CrystalDiskInfo)

*(Note on Differences: SATA SSD attribute definitions vary by manufacturer. Crucial, Kingston, and WD use `05`, `C5`, and `E7`. Samsung uses `B1`, `B3`, `B7`, `B5`, and `B6`).*

| ID (Hex) | Attribute Name | Typical Brands | Target Raw | Assessment Standard & Action |
| :---: | :--- | :--- | :---: | :--- |
| **`05`** | **Reallocated Sector Count** | Crucial, Kingston, WD | **Must be 0** | Number of bad flash blocks retired. Raw count must be **strictly 0**. |
| **`B1`** | **Wear Leveling Count** | Samsung | **Current score 80 or higher** | **Controls Samsung Health %!** Current score starts at 100 and drops as P/E cycles wear down. If Current is 51, drive health displays as 51%. Reject if health is below 70%. |
| **`B3`** | **Used Reserved Block Count (Total)** | Samsung | **Must be 0** | Number of factory reserve spare blocks consumed. Any count of 1 or higher confirms bad flash blocks have been remapped. |
| **`B4`** | **Unused Reserved Block Count (Total)** | Samsung, Crucial, Micron | High / 100 | Remaining pool of spare flash memory blocks. If normalized score drops to 0, reserve is depleted. |
| **`B5`** | **Program Fail Count (Total)** | Samsung, SanDisk | **Must be 0** | Flash memory write and programming failures. Any count of 1 or higher confirms dying flash cells. |
| **`B6`** | **Erase Fail Count (Total)** | Samsung, SanDisk | **Must be 0** | Flash block erase failures. Non-zero indicates physical block defects or failing silicon. |
| **`B7`** | **Runtime Bad Block (Total)** | Samsung | **Must be 0** | Bad flash blocks detected during active drive operation. Must be strictly 0 in a healthy drive. |
| **`BB`** | **Reported Uncorrectable** | Universal (All Brands) | **Must be 0** | Uncorrectable read errors that hardware ECC could not recover. Fatal error. |
| **`C5`** | **Current Pending Sectors** | Crucial, Kingston, WD | **Must be 0** | Unstable flash blocks awaiting reallocation. (Typically omitted on Samsung SSDs). |
| **`C7`** | **UltraDMA CRC Error Count** | Universal (All Brands) | **0 (or stable)** | Communication errors between motherboard and drive. Non-zero indicates damaged cable or oxidized connector pins. |
| **`E7`** | **SSD Life Left** | Crucial, Kingston, Intel | **80% or higher** | Wear gauge based on P/E cycles used by Crucial/Kingston. (Omitted on Samsung drives, which use B1). |
| **`EB`** | **POR Recovery Count** | Samsung, Intel | Informational | Power-Off Recovery count. Increments whenever the drive loses power without a formal OS shutdown. Normal. |

---

## 🕵️ 4. Counterfeits, Scams & Verification Tools

### Part A: M.2 NVMe Scams & Counterfeits
1. **Counterfeit Samsung 980 Pro / 990 Pro Drives:**
   * **The Scam:** Fraudulent sellers flash modified firmware to cheap DRAM-less drives (Maxio MAP1602 or Realtek RTS5765DL controllers) to report `"Samsung SSD 980 PRO 2TB"` in Windows Device Manager, then affix counterfeit Samsung labels.
   * **Verification:**
     * **Samsung Magician:** Genuine Samsung drives pass cryptographic handshake authentication. A fake drive will report **"N/A"**, **"Genuine: False"**, or display as an unsupported third-party volume with firmware updates locked.
     * **Metallic Controller Cap:** Genuine Samsung Elpis/Pascal controllers feature a shiny nickel-plated metallic cap. Counterfeits are matte black plastic.
     * **Dedicated DRAM:** Genuine 980/990 Pro drives feature a dedicated Samsung LPDDR4 chip. Fakes have empty PCB traces.

### Part B: 2.5" SATA SSD Scams
1. **The MicroSD Array Shell Scam:**
   * **The Scam:** Empty plastic 2.5" drive enclosures containing a tiny circuit board with 1 to 4 cheap microSD cards or generic USB flash modules wired to a bridge chip.
   * **Verification:**
     * **Weight:** Authentic 2.5" SATA SSDs weigh **40g–60g**. MicroSD scams weigh **under 25g–30g**.
     * **Casing Screws:** Authentic drives use precision Torx or Phillips screws. Fakes use flimsy snap-together plastic clips with visible pry marks.
     * **Write Speed:** Sustained write throughput instantly collapses to **5–15 MB/s**.

### Part C: Universal Flash Scams (Both NVMe & SATA)
1. **Capacity Spoofing & Cyclic Overwrite:**
   * **The Scam:** Controller LBA tables are modified in firmware so a 64GB or 128GB flash die advertises **2TB or 4TB**.
   * **The Hazard:** Windows writes files normally until real physical capacity is exceeded. Afterward, the controller silently wraps around, overwriting and destroying previous data while continuing to report successful writes.
   * **Detection:** Run **ValiDrive** (by GRC). It tests 576 random addresses across the entire drive in under 2 minutes and immediately highlights declared vs. phantom storage.

---

## 📋 5. Fast Countertop Decision Matrix

### Matrix A: M.2 NVMe SSD Decision Matrix

| Test Passed? | Observation / Finding | Action |
| :---: | :--- | :--- |
| ✅ | Health 90% or higher, `0E` = 0, `01` = 0, rated TBW writes below 30%, full PCIe 3.0/4.0/5.0 bus speed. | **BUY WITH CONFIDENCE** |
| ⚠️ | Health between 70% and 80%, `0E` = 0, `01` = 0, clean SMART log, stable CDM speed. | **NEGOTIATE DISCOUNT** (Safe for secondary game storage). |
| ❌ | NVMe `0E` (Media Errors) is 1 or higher (Fail). | **REJECT (Active Flash Cell Bit Rot)** |
| ❌ | NVMe `01` (Critical Warning) is non-zero (Spare exhausted, overheating, or read-only lock). | **REJECT (Dying Drive)** |
| ❌ | Negotiates at PCIe x1 or x2 instead of x4, or fails Samsung Magician (`Genuine: False`). | **REJECT (Broken Lanes / Counterfeit)** |
| ❌ | Write speed freezes at 0 MB/s during CDM burst. | **REJECT (Controller Voltage Shift Lock)** |

### Matrix B: 2.5" SATA III SSD Decision Matrix

| Test Passed? | Observation / Finding | Action |
| :---: | :--- | :--- |
| ✅ | Health 90% or higher, `05` = 0, `C5` = 0, `C7` = 0, SATA/600 link, CDM sequential exceeds 500 MB/s. | **BUY WITH CONFIDENCE** |
| ⚠️ | Health between 70% and 80%, `05` = 0, `C5` = 0, stable 500 MB/s transfer, clean SMART log. | **NEGOTIATE DISCOUNT** (Safe for secondary storage). |
| ❌ | SATA `05`, `B7`, `B3`, `B5`, or `B6` is 1 or higher (Fail) or `C5` is 1 or higher (Fail). | **REJECT (Physical Bad Flash Blocks / Program Failures)** |
| ❌ | Drive weighs under 30 grams or sounds hollow when tapped. | **REJECT (MicroSD Array Scam)** |
| ❌ | ValiDrive detects non-declared or phantom addresses. | **REJECT (Firmware Capacity Spoof)** |
| ❌ | CDM write speed collapses to 5 to 20 MB/s. | **REJECT (MicroSD Fake / Dying NAND)** |

---

**Hardware Buying & Maintenance Guides**  
Authored by **M. Hamza** ([@XBEAST1](https://github.com/XBEAST1)). For the latest updates, companion component guides, and contributions, visit the [GitHub Repository](https://github.com/XBEAST1/Laptop-And-Mobile-Buying-Guides).

