# Tech & PC Hardware Buying & Maintenance Guides

A comprehensive collection of buying guides, inspection checklists, and troubleshooting tips for mobile devices, laptops, MacBooks, and desktop PC components.

---

## ⚡ Quick 30-Minute In-Shop Inspection Protocol

When buying used components in local computer shops or marketplaces, sellers rarely allow 1+ hours of testing. You typically get **15 to 30 minutes** on a test bench.

### The Must-Bring USB Toolkit (Portable, No Install)
Carry a flash drive loaded with these portable utilities:
* **GPU-Z & CPU-Z:** Hardware specification, fake BIOS, and PCIe bus lane verification.
* **FurMark / Superposition:** Heavy 3D load, VRAM stability, and thermal stress testing.
* **CrystalDiskInfo & CrystalDiskMark:** Lifetime SMART health data, TBW wear, and burst speed validation.
* **HDDScan:** Autonomous firmware SMART Short DST, mechanical butterfly seek test, and platter surface spot check.
* **HWiNFO64:** Real-time sensor monitoring (temperature gap between core & hotspot, motherboard +12V PSU rail voltage).
* **Cinebench R23 (Portable):** Instant AVX multi-core CPU load and stability validation.
* **7-Zip (Portable):** 45-second multi-threaded memory controller, CPU cache, and RAM stability benchmark.

### Rapid Time-Budget Checklist

| Component | Time Budget | Key Tests & Verification | Walk-Away Red Flags |
| :--- | :--- | :--- | :--- |
| **GPU** | **10–12 Mins** | • Check GPU-Z bus interface (`PCIe x16 @ 3.0/4.0`, not `x1`/`x4`).<br>• Run FurMark for 8–10 mins.<br>• Verify Core stays below 75°C–80°C and Hotspot delta stays within 15°C–20°C in HWiNFO64.<br>• Inspect fan bearings at 80% speed. | Screen artifacts (colored lines/dots), instant driver crash/reboot, Hotspot exceeds 105°C, or stuck PCIe link width. |
| **CPU** | **3 Mins** | • Physical inspection: straight pins (AM4) or clean pads (LGA Intel/AM5).<br>• Verify model and core count in CPU-Z.<br>• Run 2-min CPU-Z Stress or 1 pass Cinebench R23.<br>• Run 45s 7-Zip decompression test. | Bent/missing pins, deep substrate burns, instant BSOD/freeze under load, or 7-Zip arithmetic errors. |
| **SSD** | **2 Mins** | • CrystalDiskInfo: Check Health %, Total Host Writes (TBW), and Power-On Hours.<br>• Check critical raw attributes: NVMe `0E` (Media Errors) or SATA `05`/`B7` (Bad Blocks) must be 0.<br>• Run a 1-pass 1 GiB CrystalDiskMark test. | Health below 70%, bad blocks present, or write speeds throttling down to sub-SATA speeds. |
| **HDD** | **5–8 Mins** | • Gyroscopic spin-up and sound check (no rhythmic clicking).<br>• CrystalDiskInfo: verify attributes `05`, `C5`, `C6`, `BB`, `B8`, `0A` are strictly 0.<br>• HDDScan: run 2-min SMART Short DST and Butterfly seek test.<br>• CrystalDiskMark: 1-pass sequential speed check. | Any non-zero critical attribute, repetitive clicking ("click of death"), failing Short DST, or write speed collapsing below 20 MB/s. |
| **PSU** | **2 Mins** | • Sniff test (no fishy/burnt odor) and shake test.<br>• Check weight (heavy = quality heatsinks; light = cheap junk).<br>• Check 80 Plus rating and Cultists Tier List (avoid Tier F).<br>• Confirm original modular cables are included. | Burnt/fishy odor, broken warranty seals, featherlight weight (under 1.0 kg), missing/mixed modular cables, or Tier F models. |
| **RAM** | **2 Mins** | • Inspect gold teeth and bottom SMD decoupling capacitors.<br>• Enable XMP/EXPO in BIOS; verify single cold boot.<br>• CPU-Z Memory tab: verify Frequency = MT/s ÷ 2 and Dual Channel.<br>• CPU-Z SPD tab: verify DRAM maker (Samsung/Hynix/Micron).<br>• Run 45s 7-Zip Benchmark. | Missing/chipped capacitors, boot loop / safe-mode reversion on XMP, generic/blank DRAM maker (fake heatsink), or memory errors under load. |

---

## 📚 Table of Contents

### 1. Complete Device Guides
* [**Laptop Buying Guide**](Laptop/): Complete pre-purchase and hardware inspection checklist.
  * Formats: [PDF Guide](Laptop/Laptop%20Guide.pdf) | [Word DOCX](Laptop/Laptop%20Guide.docx)
  * Portable diagnostic suite included in [`Laptop/Softwares/`](Laptop/Softwares/) (CrystalDiskInfo, CrystalDiskMark, FurMark, HWiNFO64, Dead Pixel Buddy).
* [**MacBook Buying Guide**](Macbook%20Guide/): Pre-purchase and inspection guides for Apple Silicon (M1/M2/M3/M4) and Intel MacBooks.
  * Formats: [PDF Guide](Macbook%20Guide/Macbook%20Guide.pdf) | [Word DOCX](Macbook%20Guide/Macbook%20Guide.docx)
* [**Mobile Buying Guide**](Mobile/): Complete physical and operational inspection checklist for iOS (iPhone) and Android smartphones.
  * Formats: [PDF Guide](Mobile/Mobile%20Guide.pdf) | [Word DOCX](Mobile/Mobile%20Guide.docx)

---

### 2. PC Component Buying Guides
All desktop and internal hardware guides are organized inside [`PC Components/`](PC%20Components/):

| Component | Priority | Guide Link |
| :--- | :--- | :--- |
| **Graphics Cards (GPU)** | Critical | [Universal Used GPU Inspection & Stress-Testing Guide](PC%20Components/GPU/README.md) |
| **Power Supplies (PSU)** | Critical | [Universal Used PSU Safety & Inspection Guide](PC%20Components/PSU/README.md) |
| **Solid State Drives (SSD)** | High | [Universal Used SSD Health, TBW & Anti-Counterfeit Guide](PC%20Components/SSD/README.md) |
| **Hard Drives (HDD)** | High | [Universal Used HDD Inspection & Diagnostic Guide](PC%20Components/HDD/README.md) |
| **Processors (CPU)** | Moderate | [Universal Used CPU Inspection & Multi-Core Stability Guide](PC%20Components/CPU/README.md) |
| **Memory (RAM)** | Moderate | [Universal Used RAM Health, Anti-Counterfeit & Performance Guide](PC%20Components/RAM/README.md) |

---

### 3. Maintenance & Troubleshooting
* [**Hardware Maintenance, Fixes & Cleaning Guide**](Maintenance%20&%20Troubleshooting/README.md)
  * **RAM, SSD (M.2 & SATA) & SD Card Contact Cleaning:** Reviving unbootable RAM sticks, restoring degraded M.2 PCIe link speeds, fixing SATA SSD disconnects, and reviving unreadable SD/MicroSD cards using the pencil eraser technique.
  * **HDD Contact Pad & Pin Cleaning:** Restoring oxidized external SATA connector pins and internal PCB contact pads (soft eraser vs. precision needle scraping) to fix CRC errors (`C7`), clicking, and spin-up failures.
  * **GPU & PCIe Gold Fingers:** Cleaning PCIe edge contacts to fix display artifacts and connection drops.
  * **General Maintenance:** Safe dusting, fan cleaning, and thermal paste re-application.
  * **Motherboard Logo Freeze / CMOS Reset:** Unfreezing motherboards permanently stuck on manufacturer splash screens.

---

## Contributing & Feedback
Feel free to open an issue or pull request if you want to suggest new hardware sections, tips, or updates to existing guides!
