# Universal Used HDD Inspection & Diagnostic Guide

A fast, practical, field-tested guide for evaluating used mechanical hard disk drives (3.5" desktop/NAS/enterprise & 2.5" laptop/portable, 500GB to 20TB+).

Designed for a strict **10-minute in-shop counter triage** using portable diagnostic utilities (CrystalDiskInfo, HDDScan, CrystalDiskMark) to detect physical bad sectors, mechanical spindle wear, and wiped SMART tables before handing over payment.

---

## 🚫 1. Instant Dealbreakers (Walk Away Immediately)

If a drive triggers **ANY** of these 6 conditions at the seller's counter, **reject it immediately**:

1. **Abnormal Acoustic & Mechanical Sounds:**
   * Any repetitive rhythmic clicking ("click of death"), metallic scraping, chirping, or grinding noises during spin-up or read.
   * Indicates collapsed spindle bearings or actuator heads crashing against magnetic platters.
2. **Critical CrystalDiskInfo Health Warnings:**
   * CrystalDiskInfo reports **Caution** (yellow) or **Bad** (red).
   * Uncorrectable error flags tripped in firmware telemetry.
3. **Critical S.M.A.R.T. Errors (Raw Value MUST be strictly 0):**
   * **`05` Reallocated Sectors (Must be 0):** Any count of 1 or higher confirms permanent physical bad sectors remapped to spare tracks.
   * **`C5` Current Pending Sectors (Must be 0):** Any count of 1 or higher indicates active unstable, unreadable sectors awaiting remap.
   * **`C6` Offline Uncorrectable (Must be 0):** Any count of 1 or higher confirms permanent platter surface damage confirmed by background scan.
   * **`BB` Reported Uncorrectable (Must be 0):** Fatal read failures *(Warning: Drive can still show a blue "Good" badge even with BB of 1 or higher!)*.
   * **`0A` Spin Retry Count (Must be 0):** Any count of 1 or higher indicates the spindle motor failed to reach rated speed on first attempt (failing motor or bearings).
   * **`B8` End-to-End Error (Must be 0):** Any count of 1 or higher indicates parity corruption between onboard cache RAM and controller (failing logic board).
4. **Thermal Warning & Idle Overheating:**
   * Operating temperature exceeds **50°C** while idling or under light bench testing.
   * Indicates degraded spindle motor drawing excessive current or dried bearing lubricant.
5. **Slow Platter Blocks & Latency Spikes:**
   * Any **Red (exceeds 500ms latency)** or **Blue/Black (Bad)** block detected during an HDDScan surface spot check.
   * Confirms weak magnetic signal or unreadable physical sectors.
6. **Throughput Collapse & Actuator Thrashing:**
   * Sequential write speed collapses and stays pinned at **10–20 MB/s**, or system completely freezes during transfers.
   * Confirms drive is stuck in emergency head recalibration and read-retry loops.

---

## ⚡ 2. The 10-Minute Shop Field Test

Everything needed for a fast counter inspection is covered by three free portable Windows tools:
- **CrystalDiskInfo (CDI):** Health, S.M.A.R.T. audit, and interface check.
- **HDDScan:** Autonomous firmware self-tests, surface latency, and mechanical stress.
- **CrystalDiskMark (CDM):** Sustained sequential throughput check.

```
[10-MINUTE COUNTER WORKFLOW]
Physical & Sound Check (1m) ──> CrystalDiskInfo Audit (2m) ──> HDDScan Short DST & Butterfly (4m) ──> CrystalDiskMark SEQ (1m) ──> DECISION
```

### Step 1: Physical & Acoustic Check (1 Minute, No Software)
1. **Visual:** Inspect casing corners for drop dents, Torx screws for tampering/opening, and SATA pins for oxidation or cracks.
2. **Gyroscopic & Sound Check:** Connect drive and hold gently by the edges during spin-up:
   - Must feel a smooth gyroscopic hum without violent vibration.
   - Listen closely: expect a smooth acceleration and a single head unpark click.
   - **Reject immediately** if you hear repetitive rhythmic clicking ("click of death"), metallic scraping, or high-pitched screeching.

### Step 2: CrystalDiskInfo Decimal Audit (2 Minutes)
1. Open **CrystalDiskInfo** with Administrator privileges.
2. **Crucial Setup Step:** Switch Raw values to decimal:
   $$\text{Function} \longrightarrow \text{Advanced Feature} \longrightarrow \text{Raw Values} \longrightarrow \mathbf{10\text{ [DEC]}}$$
   *(Default Hexadecimal disguises severe errors: raw hex `0x0000000A` looks minor but represents 10 physical bad or pending sectors!).*
3. Verify all **Instant Dealbreakers** (`05`, `C5`, `C6`, `BB`, `B8`, `0A`) are **strictly 0**.
4. Check **Transfer Mode:** Must report **SATA/600 | SATA/600** (SATA III). *(Note: If your USB dock/adapter is SATA II, it will show SATA/300. Ensure the drive itself supports SATA/600).*
5. Check **Power-On Hours (Age):**
   - *Consumer (BarraCuda, WD Blue):* Safe if **below 20,000 hours**.
   - *Enterprise / NAS (Exos, IronWolf, WD Red Plus/Gold):* Safe if **below 35,000 hours**.
   - *Wipe Alert:* If a 6-year-old drive reports under 50 hours, its S.M.A.R.T. table was wiped with professional tools.
6. Check **Features Bar:** Look for **`TRIM`**. If present, the drive uses **SMR** (Shingled Magnetic Recording).

### Step 3: HDDScan Firmware & Mechanical Check (3–4 Minutes)
1. **Autonomous Firmware Test (SMART Short Test, 1 to 2 min):**
   - In HDDScan, select the drive:
     $$\text{Tests} \longrightarrow \mathbf{\text{SMART Offline Short Test}}$$
   - This executes an autonomous internal hardware self-test inside drive firmware (evaluates preamp, voice coil motor, and electronics independently of Windows).
   - Must finish with **`Status: Completed without error`**. Reject if it reports read, servo, or electrical faults.
2. **Mechanical Actuator Test (Butterfly Read Test, 1 to 2 min):**
   - In HDDScan:
     $$\text{Tests} \longrightarrow \mathbf{\text{Butterfly Read Test}}$$
   - Rapidly swings heads between outer and inner tracks across full platter stroke.
   - Listen closely: must run smoothly with **NO loud rhythmic clacking or freezing**.
3. **Quick Outer-Track Surface Spot Check (1 min):**
   - In HDDScan (Block size: 256):
     $$\text{Tests} \longrightarrow \mathbf{\text{Read Surface Test}}$$
   - Run for just the first 2–3% of the drive.
   - Must be overwhelmingly **White (under 5ms)** and **Light Gray (under 20ms)**. **Zero Red or Bad blocks allowed.**

### Step 4: CrystalDiskMark Sequential Speed Check (1 Minute)
*(Never run default 5-pass / All-row benchmarks on mechanical HDDs. Random 4K tests take 20+ minutes and thrash drive actuator heads needlessly).*

1. Set Test Size: **`1 GiB`**.
2. Set Passes: **`1`** (change `5` to `1`).
3. Click ONLY the top **`[SEQ1M Q8T1]`** button for a 30-second sustained speed check:
   * **7200 RPM Enterprise 3.5" (8TB–20TB+):** **Exceeds 200 MB/s** (Fail if below 160 MB/s)
   * **7200 RPM Desktop 3.5" (1TB–6TB):** **Exceeds 150 MB/s** (Fail if below 120 MB/s)
   * **5400 / 5900 RPM Desktop/NAS 3.5":** **Exceeds 110 MB/s** (Fail if below 90 MB/s)
   * **5400 RPM Laptop 2.5":** **Exceeds 85 MB/s** (Fail if below 70 MB/s)
   * *(Note: Speeds naturally decline by roughly 50% toward the end of the drive due to ZBR platter geometry).*

---

## 📊 3. Master S.M.A.R.T. Reference Table (All 22 Attributes)

### Understanding the 4 Telemetry Columns
- **Current (Norm):** Present health score (starts at 100 or 200). Drops as the drive wears out. **Higher is better ↑**.
- **Worst (Norm):** All-time lowest score the drive ever hit. Never resets. **Higher is better ↑**.
- **Threshold:** Factory minimum floor. *(Never rely on this alone; OEM thresholds are set very low for warranty claims)*.
- **Raw Value (10 [DEC]):** The actual physical event counter. For errors: **Lower is better ↓ (Strictly 0)**.

---

### Complete Attributes Reference

| ID | Attribute Name | Current | Worst | Threshold | Target Raw (10 [DEC]) | Directionality | Assessment Standard & Action |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **01** | Raw Read Error Rate | 100–200 | 100–200 | 6–51 | 0 (WD/HGST/Tosh) / High (Seagate)* | Norm: **Higher ↑**<br>Raw: **Lower ↓** | Raw must be **0** on WD, HGST, and Toshiba (**reject if 1 or higher**). *Seagate note below. |
| **03** | Spin-Up Time | 85–200 | 85–200 | 0–25 | • 2.5" Laptop: 1,000–2,500 ms<br>• 3.5" (1–3 platters): 2,500–5,000 ms<br>• 3.5" High-Cap (4–10 platters): 5,000–9,500 ms | Norm: **Higher ↑**<br>Raw: **Lower ↓** | Milliseconds to reach full RPM. Abnormally high ms indicates motor bearing friction or weak 12V power. |
| **04** | Start/Stop Count | 90–100 | 90–100 | 0–20 | Below 5,000–10,000 | Norm: **Higher ↑**<br>Raw: **Lower ↓** | Total spindle start/stop cycles. Consumer rated 30k–50k; Enterprise rated 10k. |
| **05** | Reallocated Sectors Count | 100–200 | 100–200 | 10–140 | **0** | Norm: **Higher ↑**<br>Raw: **Lower ↓ (0)** | **CRITICAL: Instant Reject if Raw is 1 or higher.** Physical bad sectors retired to spare tracks. Platter rot. |
| **07** | Seek Error Rate | 60–200 | 60–200 | 30–51 | 0 (WD/HGST) / High (Seagate)* | Norm: **Higher ↑**<br>Raw: **Lower ↓** | Head positioning errors. Raw must be **0** on WD/HGST. *Seagate normalized 60–88 is pristine. |
| **09** | Power-On Hours (POH) | 50–100 | 50–100 | 0 | Below 15,000–20,000 (Desktop)<br>Below 35,000 (Enterprise) | Norm: **Higher ↑**<br>Raw: **Lower ↓** | Total active hours run. Cross-check against label manufacturing date to catch wiped SMART tables. |
| **0A** | Spin Retry Count | 100–200 | 100–200 | 50–97 | **0** | Norm: **Higher ↑**<br>Raw: **Lower ↓ (0)** | **CRITICAL: Instant Reject if Raw is 1 or higher.** Motor failed to reach speed on first attempt. Bearing wear. |
| **0C** | Power Cycle Count | 90–100 | 90–100 | 0–20 | Below 1,500–3,000 (Desktop)<br>Below 500 (Enterprise) | Norm: **Higher ↑**<br>Raw: **Lower ↓** | Total cold boots. If 04 far exceeds 0C, the drive was subjected to aggressive sleep/spindown cycles. |
| **B7** | SATA Downshift Count *(Vendor Specific)* | 95–100 | 95–100 | 0 | 0 (or low static count) | Norm: **Higher ↑**<br>Raw: **Lower ↓** | Link speed downshifts (e.g., SATA III to SATA II) caused by cable noise, oxidized port, or dock limits. |
| **B8** | End-to-End Error (IOEDC) | 100 | 100 | 36–99 | **0** | Norm: **Higher ↑**<br>Raw: **Lower ↓ (0)** | **CRITICAL: Instant Reject if Raw is 1 or higher.** Data corrupted between drive cache RAM and controller. Failing PCB. |
| **BB** | Reported Uncorrectable | 100 | 100 | 0 | **0** | Norm: **Higher ↑**<br>Raw: **Lower ↓ (0)** | **CRITICAL: Instant Reject if Raw is 1 or higher.** Number of uncorrectable read errors where hardware ECC failed. |
| **BC** | Command Timeout | 100 | 99–100 | 0 | 0 (WD/Tosh/HGST) / Low (Seagate) | Norm: **Higher ↑**<br>Raw: **Lower ↓** | Aborted operations due to drive freeze. Reject if counter increases during benchmark testing. |
| **BD** | High Fly Writes | 90–100 | 70–100 | 0 | 0 (Ideal) / Under 20 (Server chassis) | Norm: **Higher ↑**<br>Raw: **Lower ↓** | Head drifted outside safe height during write. High values indicate drops, shock, or bearing flutter. |
| **BE / C2** | Airflow / Drive Temp | 50–75 (BE)<br>100–200 (C2) | 40–60 (BE)<br>Max Temp (C2) | 0–45 | 25°C–45°C | Norm: **Higher ↑**<br>Raw: **Nominal (25°C–45°C)** | Real-time temperature. Reject if idle temp exceeds 50°C or if historical max (Worst) exceeded 60°C. |
| **C1** | Load/Unload Cycles | 80–100 | 80–100 | 0 | Under 100k (3.5") / Under 300k (2.5") | Norm: **Higher ↑**<br>Raw: **Lower ↓** | Head ramp parking cycles. Laptop rated 600k; Desktop rated 300k. WD runs high due to 8s idle timer. |
| **C3** | Hardware ECC Recovered | 100–200 (WD)<br>1–100 (Seagate) | 100–200 (WD)<br>1–75 (Seagate) | 0 (or 15) | 0 (WD/HGST) / High (Seagate)* | Norm: **Higher ↑**<br>Raw: **Lower ↓ (WD) / N/A (Seagate)** | On-the-fly ECC corrections. High raw on Seagate mirrors ID 01 (counts total sector operations). Normalized drops to 1 if historical uncorrectable errors (BB) occurred. |
| **C5** | Current Pending Sector | 100–200 | 100–200 | 0 | **0** | Norm: **Higher ↑**<br>Raw: **Lower ↓ (0)** | **CRITICAL: Instant Reject if Raw is 1 or higher.** Active unreadable sectors awaiting remap. Causes freezes. |
| **C6** | Offline Uncorrectable | 100–200 | 100–200 | 0 | **0** | Norm: **Higher ↑**<br>Raw: **Lower ↓ (0)** | **CRITICAL: Instant Reject if Raw is 1 or higher.** Uncorrectable bad sectors found during background scan. |
| **C7** | UltraDMA CRC Errors | 100–200 | 100–200 | 0 | 0 (Ideal) / Static count | Norm: **Higher ↑**<br>Raw: **Lower ↓ (Static)** | SATA bus errors (more than 95% caused by bad cables). Harmless if count stays static. Reject if count increases during test. |
| **F0** | Head Flying Hours | 100 | 253 | 0 | Active flying hours | Norm: **Higher ↑**<br>Raw: **Lower ↓** | Hours heads actively spent flying over platters (ID 09 = total powered time; F0 = mechanical flight time). |
| **F1** | Total Host Writes | 100 | 253 | 0 | Cumulative written sectors | Norm: **Higher ↑**<br>Raw: **Lower ↓** | Lifetime sectors written. Multiply raw sectors by 512 bytes to get approximate Gigabytes written. |
| **F2** | Total Host Reads | 100 | 253 | 0 | Cumulative read sectors | Norm: **Higher ↑**<br>Raw: **Lower ↓** | Lifetime sectors read by the operating system. |

---

### Crucial Inspection Notes

- **The "Used Drive Trap" & False "Good" Status:**
  CrystalDiskInfo only turns "Bad" or "Caution" when Current drops to or below Threshold. 
  - On many modern drives (especially Seagate), critical attributes like **ID BB (Reported Uncorrectable Errors)** have a factory **Threshold of `0`**.
  - A drive can have **Current = 1 and hundreds of fatal uncorrectable errors (`BB Raw = 205`)**, yet CrystalDiskInfo will **falsely display a bright blue "Good" badge**!
  - **Rule When Buying:** Never rely on the blue "Good" badge alone. If **ID BB is 1 or higher** or **ID 05 is 1 or higher**, do not buy.
- **Seagate Raw Values Quirk (IDs 01, 07, C3):**
  Seagate packs two values into the raw 48-bit field: the top 16 bits are error counts, and the bottom 32 bits are total operations. In decimal view, this displays as millions or billions on a 100% healthy drive.
  - Check **Normalized Current**: On Seagate, normalized values use a logarithmic scale of recent operations. Pristine drives typically show **70–88 for ID 01** and **60–88 for ID 07** (any value well above the single-digit threshold indicates zero recent errors). (On WD/HGST/Toshiba, 01/07 normalized sits at 100 or 200).
  - In Hex view (`16 [HEX]`), the first four digits must be `0000`.
- **Why Modern Drives Have Extra Attributes (B7, F0, F1, F2):**
  The ATA specification allows manufacturers to add proprietary diagnostic telemetry (such as link downshifts on B7, active flying hours on F0, and host write/read volume on F1/F2). Seeing extra attributes is completely normal.
- **UltraDMA CRC (C7) Test:**
  Note the starting value. Run a benchmark. If the count remains unchanged, the drive is completely healthy (past bad cable). If it increases during testing with a known-good cable, the drive's SATA port or onboard controller is broken.

---

## 🕵️ 4. Counterfeits, Wiped SMART & Used Market Traps

### 1. Firmware-Wiped S.M.A.R.T. Tables (The "Zero-Hour" Trap)
* **The Scam:** Shady recyclers use hardware flashing tools (e.g., PC-3000, specialized vendor serial terminal commands) to reset Power-On Hours (`09`), Power Cycles (`0C`), and reallocated sector logs back to zero, presenting heavily degraded server drives as "brand new" or "lightly tested".
* **How to Catch It Instantly:**
  * **The Label vs. Telemetry Mismatch:** Look at the manufacturing date printed on the drive's top metallic label. If an enterprise drive manufactured in **2017 or 2019** claims to have only **25 or 100 hours** of power-on time, its SMART table was deliberately wiped.
  * **Reprinted / Fake Labels:** Check the label quality. Genuine OEM labels have crisp, microscopic micro-text and laser-etched QR codes/data matrices. Counterfeit labels often feel like thick paper stickers with blurry font edges pasted directly over original barcodes.

### 2. The "Chia Coin" Crypto Mining Burnout
* **The Trap:** During the 2021–2022 crypto boom, hard drives were used for intense 24/7 cryptographic "plotting", writing hundreds of terabytes continuously and wearing down voice-coil motor bearings and servo arms prematurely.
* **How to Catch It:**
  * Check **Total Host Writes (`F1`)**: A standard 5-year-old desktop drive rarely exceeds 50–100 TB written; Chia plotting drives often show massive multi-petabyte write counters.
  * Listen for bearing wear: Chia-thrashed drives often exhibit excessive high-frequency motor whine or loose, rattly seeks during the HDDScan Butterfly Test.

### 3. Disguised Surveillance & Server Pulls
* **The Trap:** Sellers sell high-vibration, high-noise server SAS/SATA pulls (with 40,000+ continuous hours) relabeled as quiet consumer drives (e.g., WD Blue or Seagate BarraCuda).
* **The Rule:** Always verify the exact model number reported inside **CrystalDiskInfo firmware string**, not just the paper sticker.

---

## ⚙️ 5. SMR vs. CMR Platter Architecture & Storage Classes

### CMR (Conventional Magnetic Recording) vs. SMR (Shingled Magnetic Recording)
* **CMR (The Gold Standard):** Magnetic tracks sit side-by-side with guard spaces. Data can be written or updated directly without disturbing neighboring tracks. Sustains steady **150–250 MB/s** writes across the entire drive. Essential for OS drives, NAS arrays, RAID, and active gaming storage.
* **SMR (The Budget Trap):** Magnetic tracks overlap like shingles on a roof to squeeze higher density onto cheaper platters. Writing to one track requires reading, caching, and rewriting neighboring overlapping tracks.
  * **The SMR Performance Cliff:** SMR drives rely on a fast "media cache" buffer. Once continuous writes exceed 15–30 GB, the buffer fills and write speeds **collapse down to 10–25 MB/s** (slower than an old USB 2.0 thumb drive!).
  * **How to Spot SMR Instantly:** In CrystalDiskInfo, look at the **Supported Features** bar. If a mechanical hard drive lists **`TRIM`**, it is **guaranteed to be an SMR drive** (TRIM is required for SMR zone garbage collection).

### Hard Drive Storage Classes
* **Desktop Class (WD Blue, Seagate BarraCuda):** Budget 5400/7200 RPM drives (capacities from 2TB to 6TB are predominantly SMR). Best only for basic secondary media archival.
* **NAS Class (WD Red Plus / Pro, Seagate IronWolf):** 100% CMR, rated for 24/7 multi-drive operation with rotational vibration (RV) sensors.
* **Enterprise Class (Seagate Exos, WD Gold / Ultrastar):** Flagship 7200 RPM helium-sealed drives (10TB+), rated for 550 TB/year workloads and 2.5 million hours MTBF. Run slightly warmer and produce audible mechanical seek clatter, but offer maximum endurance.

---

## 📋 6. Fast Countertop Decision Matrix

| Test Passed? | Observation / Finding | Action |
| :---: | :--- | :--- |
| ✅ | 05, C5, C6, BB, B8, 0A all strictly 0; short DST passes; smooth butterfly seek; nominal speeds. | **BUY WITH CONFIDENCE** |
| ⚠️ | C7 count is above 0 (static historical CRC error), POH between 20k–35k hrs on enterprise drive, passes all tests. | **NEGOTIATE DISCOUNT** (Safe for secondary non-critical storage). |
| ❌ | Any critical attribute (05, C5, C6, BB, 0A, B8) is 1 or higher (Fail). | **REJECT (Platter Rot / Bad Sectors)** |
| ❌ | HDDScan SMART Short Test fails or aborts with electrical/servo errors. | **REJECT (Firmware / Hardware Defect)** |
| ❌ | Rhythmic repetitive clicking ("click of death") or violent vibrating during spin-up. | **REJECT (Head Crash / Motor Bearing Failure)** |
| ❌ | CrystalDiskMark write speed collapses and stays stuck under 20 MB/s. | **REJECT (Degraded Surface / SMR Zone Collapse)** |
| ❌ | 5+ year old drive reporting under 100 Power-On Hours on CrystalDiskInfo. | **REJECT (Wiped S.M.A.R.T. Counter Fraud)** |
