# Hardware Maintenance, Fixes & Cleaning Guide

Practical troubleshooting tips, cleaning procedures, and quick hardware fixes for common PC components.

---

## General Safety & Precautions

1. **Power Off & Unplug:** Always switch off the power supply and disconnect the power cord before opening or handling any hardware.
2. **Discharge Residual Power:** Press and hold the power button for 10–15 seconds after unplugging to drain residual capacitor charge.
3. **Static Electricity (ESD):** Touch a bare metal part of the PC case or use an anti-static wrist strap before handling sensitive circuit boards.
4. **Cleaners to Use:** 
   - High-purity **Isopropyl Alcohol (90% to 99% IPA)**.
   - Clean, soft pencil eraser (white vinyl erasers are best; avoid abrasive ink erasers).
   - Lint-free microfiber cloths or cotton swabs (Q-tips).
   - Never use tap water, glass cleaners, or household solvents on electronics.

---

## 1. RAM, SSDs (M.2 & 2.5" SATA) & SD / MicroSD Cards: Contact Cleaning with an Eraser

### A. RAM (Desktop & Laptop Memory)
#### Symptoms of Dirty / Oxidized RAM Contacts:
* PC turns on (fans spin), but there is **no display / no POST**.
* Motherboard emits memory error beeps (e.g., continuous beeps or 3 beeps depending on BIOS).
* Random Blue Screen of Death (BSOD) crashes (e.g., `MEMORY_MANAGEMENT`).
* System shows less RAM than installed or fails memory tests.

#### Cleaning Steps:
1. **Remove the RAM:** Unlatch the retention clips on the motherboard RAM slot and gently pull the stick straight out.
2. **Inspect the Gold Contacts:** Look closely at the gold pins ("fingers") along the bottom edge for dust, grime, or dark tarnish (oxidation).
3. **Use a Soft Pencil Eraser:**
   - Place the RAM stick on a clean, flat, non-conductive surface.
   - Lightly rub the gold pins on both sides with a clean white eraser in one direction (towards the outer edge).
   - You will see dark oxidation residue lift off onto the eraser.
4. **Remove Eraser Crumbs:** Thoroughly wipe the contacts with a lint-free cloth or a cotton swab lightly dipped in 90% or higher isopropyl alcohol to remove all rubber shavings.
5. **Clean the Motherboard Slot:** Use a can of compressed air or a soft dry brush to blow out dust from the motherboard RAM slot.
6. **Reinstall & Test:** Re-seat the RAM firmly until both side clips click shut.

### B. M.2 NVMe SSDs (PCIe Edge Contacts)
#### Symptoms of Dirty / Oxidized M.2 Contacts:
* SSD suddenly disappears from Windows ("Drive not found" in File Explorer or BIOS).
* Drive negotiates at degraded PCIe lane widths (e.g., `PCIe 4.0 x1` or `x2` instead of full `x4` in CrystalDiskInfo / HWiNFO64), cutting read/write performance in half.
* CrystalDiskInfo reports a non-zero count (1 or higher) for NVMe attribute **`0F` (Error Information Log Entries)** while attribute **`0E` (Media and Data Integrity Errors)** remains 0 (Must be strictly 0 in a healthy drive). This contrast confirms physical interface connection drops or PCIe bus transmission errors due to oxidized contacts, rather than dying flash memory cells.
* Random Windows freezes, sudden system lockups, or `CRITICAL_PROCESS_DIED` BSODs.

#### Cleaning Steps:
1. **Remove the M.2 SSD:** Unscrew the M.2 retaining screw or release the plastic latch, then pull the drive gently out at a 30° angle.
2. **Inspect the Gold Edge Pins:** Look at the small gold contacts on both sides of the M.2 keyed notch for flux residue, fingerprints, or gray oxidation film.
3. **The Eraser Rub:**
   - Place the M.2 drive flat on a clean surface.
   - Lightly rub the gold edge contacts on both sides with a clean, soft white eraser towards the outer edge.
   - You will see dull, oxidized pins turn bright and shiny gold.
4. **Clean Residue:** Thoroughly wipe the contacts with a cotton swab dampened with 90% or higher Isopropyl Alcohol to remove all eraser crumbs and skin oils.
5. **Reinstall:** Blow any dust out of the motherboard M.2 slot with compressed air, reinsert the SSD firmly into the slot, and secure the screw.

### C. 2.5" SATA SSDs (External SATA Data & Power Contacts)
#### Symptoms of Dirty / Oxidized 2.5" SATA SSD Pins:
* Drive intermittently disconnects or fails to appear in BIOS/Windows until the SATA cable is wiggled.
* CrystalDiskInfo reports that **Attribute `C7` (UltraDMA CRC Error Count) is 1 or higher** (Raw value must be 0 in a healthy drive). A non-zero count indicates data packet corruption across the physical SATA bus connection.
* Large file copies freeze, stall, or collapse to 0 MB/s due to SATA interface retry loops.

#### Cleaning Steps:
1. **Inspect the External Ports:** On the rear edge of the 2.5" SATA SSD casing, inspect the "L"-shaped plastic SATA Data port (7 gold signal pins carrying high-speed differential data) and SATA Power port (15 gold power pins carrying +3.3V, +5V, and +12V power rails). Over time, dust, grease, and oxidation create a dull, non-conductive film over these contacts.
2. **The Eraser Technique:**
   - Cut a small narrow wedge or angled tip off a clean white vinyl pencil eraser.
   - Gently insert the narrow eraser edge into the L-shaped slot and rub back and forth across the flat gold pins until bright, shiny gold is restored.
3. **Clean Debris:** Dip a cotton swab in **90% or higher Isopropyl Alcohol**, wipe the pins thoroughly to remove all rubber shavings, and let it dry for 60 seconds.
4. **Cable Check:** If Attribute `C7` (UltraDMA CRC Error Count) raw count continues to increase above 0 after cleaning, the SATA data cable is faulty or loose. Replace the SATA data cable.

### D. SD Cards, MicroSD Cards & Adapters
#### Symptoms of Oxidized Flash Contacts:
* Card reader throws *"Card not recognized"*, *"Please insert a disk"*, or *"You need to format the disk before you can use it"*.
* Sudden disconnection or read/write I/O errors during large file transfers.
* Camera, drone, or smartphone intermittently reports *"No SD card inserted"*.

#### Cleaning Steps:
1. **Inspect the Contacts:** Examine the small gold pins on the back of the SD card or MicroSD card. Over time, skin oils and atmospheric moisture create a dull, cloudy film of oxidation.
2. **The Eraser Rub:**
   - Place the memory card flat on a hard, clean table (support it firmly with your finger so thin MicroSD cards do not bend or snap).
   - Take a clean, soft white vinyl pencil eraser and gently rub across the gold pins.
   - The dull tarnish will lift off quickly, exposing bright, reflective gold contacts.
3. **Clean Residue:** Wipe away all rubber shavings thoroughly with a microfiber cloth or a cotton swab dampened with 90% or higher Isopropyl Alcohol.
4. **Adapter Check:** If using a MicroSD-to-SD adapter, the internal spring pins can also oxidize. Lightly insert and remove the MicroSD card 5–10 times to mechanically scrub internal contacts, or swap out the adapter.

---

## 2. Hard Drives (HDD): PCB Pin & Contact Pad Cleaning

### Symptoms of Oxidized HDD Contacts:
* Drive is not detected in BIOS or Windows Disk Management.
* Drive powers up, spins, and clicks or spins down abruptly.
* Intermittent disconnection, frozen file transfers, or sudden I/O device errors.
* CrystalDiskInfo reports that **Attribute `C7` (UltraDMA CRC Error Count) is 1 or higher** (Raw value must be 0 in a healthy drive). A non-zero count indicates data packet corruption across the physical SATA bus connection.

### Cleaning Steps:

#### Step 1: Clean the External SATA Cable Connection Pins (No Disassembly)
Before unscrewing the drive, inspect the rear edge where the SATA data and power cables connect:
1. **Inspect the External Ports:** Look inside the "L"-shaped plastic SATA Data port (7 gold signal pins) and SATA Power port (15 gold power pins delivering +5V and +12V power rails to the drive motor and logic board). In older, humid, or dusty PCs, these gold pins become coated in a dark, non-conductive film of dust, grease, and oxidation.
2. **The Eraser Technique:**
   - Cut a small narrow wedge or angled tip off a clean white vinyl pencil eraser.
   - Gently insert the narrow eraser edge into the L-shaped slot and rub back and forth across the flat gold pins until bright, shiny gold is restored.
3. **Clean Debris:** Dip a cotton swab (Q-tip) in **90% or higher Isopropyl Alcohol**, wipe the pins thoroughly to remove all rubber shavings, and let it dry for 60 seconds.
4. **Cable Check:** If Attribute `C7` (UltraDMA CRC Error Count) raw count continues to increase above 0 after cleaning, the internal metal springs of the SATA data cable itself are worn or oxidized. Replace the SATA data cable.

#### Step 2: Unscrew & Lift the PCB (For Internal Spindle & Head Contacts)
1. **Remove the HDD:** Disconnect SATA power and data cables, and remove the hard drive from the chassis.
2. **Locate the PCB Screws:** On the underside of the HDD, inspect the green/blue circuit board. It is typically held by Torx screws (usually T6, T8, or T9).
3. **Unscrew & Lift the PCB:**
   - Carefully remove all screws using the correct Torx screwdriver bit.
   - Gently lift the PCB off the drive body.
   - *Note:* Do **NOT** open the sealed metallic drive casing. Only remove the external PCB.
4. **Inspect the Drive Body & PCB Connection Points:**
   - On the cast-metal drive body (the black aluminum base), locate the two sets of contact pins:
     - **The Spindle Motor Pins:** Usually 3 or 4 spring pins near the center spindle motor hub (delivering multi-phase motor drive power to spin the platters).
     - **The Head Actuator / Preamp Pins:** A group of 12 to 20 spring pins near the edge of the drive that connect directly to the read/write head preamplifier inside the sealed chamber.
   - On the underside of the removed PCB, you will see the matching copper/gold contact pads that press against these pins.
   - **The Problem:** Over 3 to 10 years or more, atmospheric sulfur and humidity turn these contact pads from bright gold/copper into a dull, non-conductive dark gray or charcoal-black crust of oxidation.
5. **Clean the Contact Pads:**
   - **Level 1: The Soft Eraser Method (Light Oxidation):**
     - Gently rub the contact pads on the PCB with a clean white vinyl pencil eraser. Light oxidation will lift off quickly, revealing clean copper/gold underneath.
   - **Level 2: The Needle / Sharp Object Technique (Severe, Hardened Black Oxidation):**
     - If the black coat of oxidation is too thick, hardened, or calcified, a rubber eraser will slip over it without penetrating.
     - Take a clean, sharp fine point, such as a **sewing needle, safety pin, or fine hobby blade tip**.
     > [!WARNING]
     > **Never rub horizontally across multiple contacts!** Horizontal scraping can score across insulation gaps, gouge neighboring circuit traces, or drag conductive copper burrs across contacts, causing electrical shorts.
     - **Clean One-by-One Vertically:** Very gently scratch along each contact pad individually in the lengthwise direction of the pad, carefully peeling and shaving off only the crusty black oxide layer until clean, shiny metal is exposed.
6. **Clean the Drive Body Pins & Wipe Down with IPA:**
   - Inspect the spring pins sticking out of the drive body. If their contact tips have black oxidation, very lightly polish the tips with a dry cotton swab or a gentle touch with the needle tip.
   - Thoroughly wipe both the PCB pads and the spring pins with a cotton swab dampened with **90% or higher Isopropyl Alcohol** to wash away all dislodged black oxide particles and metal dust.
   - Let it dry completely for 1–2 minutes.
7. **Reassemble & Test:** Place the PCB back into its exact position and tighten the screws evenly in a criss-cross pattern. Reconnect SATA cables and power on the drive. In many cases, previously "dead" or clicking drives will spin up and detect immediately.

---

## 3. GPU & PCIe Expansion Cards: Gold Finger Cleaning

### Symptoms of Dirty / Oxidized PCIe Contacts:
* **"No Signal" / Black Screen:** PC powers on and GPU fans spin (often ramping to 100% full speed), but the monitor displays *"No Signal"* or the motherboard VGA debug LED stays illuminated.
* **Degraded PCIe Bus Link Width (The x1 / x4 Trap):** The GPU works, but GPU-Z reports **`PCIe x16 @ x1 1.1/3.0`** or **`PCIe x16 @ x4`** instead of full **`PCIe x16 3.0/4.0`**, cutting memory bandwidth and causing severe stuttering and 1% low FPS drops in games.
* **Random Driver Crashes & Artifacts:** Frequent *"Display driver nvlddmkm / amdkmdag stopped responding and has recovered"* errors, sudden checkerboard artifacts, or black-screen resets under light 3D loads due to signal integrity loss across PCIe differential pairs.
* **Cold-Boot Intermittent Detection:** System randomly fails to detect the graphics card on startup, requiring physical wiggling or pressing of the GPU to get a display.

---

### Safe Removal & Preparation:
1. **Power Down & Discharge:** Turn off the PSU rocker switch (`O`), unplug the AC power cord, and hold the case power button for 15 seconds to drain residual power.
2. **Disconnect Cables:** Unplug monitor display cables (DisplayPort / HDMI) and unlatch the auxiliary PCIe power connectors (standard 6-pin delivering 75W, 8-pin delivering 150W, or 12V-2x6 / 12VHPWR 16-pin delivering up to 600W at 12 volts).
3. **Unscrew Case Brackets:** Remove the screws securing the GPU rear metal I/O bracket to the chassis.
4. **Release the PCIe Slot Latch:** Reach behind the card near the motherboard and press down/push open the plastic PCIe retention lock (latch).
   > [!WARNING]
   > Never yank or pull a GPU forcefully without opening this latch. Forcing it will tear the retention hook off the graphics card PCB or snap the motherboard PCIe slot housing.
5. **Pull Straight Out:** Grip the GPU firmly by the edges and pull it straight out perpendicular to the motherboard.

---

### Step-by-Step Cleaning Procedure:

#### 1. Inspect the Gold Fingers (Contacts)
* Place the GPU on a clean, flat, non-conductive surface (support the metal bracket so the heavy heatsink doesn't put pressure on the fans).
* Examine the 164 gold teeth along both sides of the PCIe edge connector under bright light for fingerprints, oily flux, or dull grayish oxidation.

> [!NOTE]
> **The "Shorter Pin" Factory Design:** Look closely at the PCIe connector. You will notice that **Pin B17** (and Pin A1 or Pin B31 on some cards) is noticeably shorter than the other pins. This is **100% intentional factory engineering** (Hot-Plug Presence Detect `PRSNT2#`) designed as an electrical sense pin so the motherboard detects card insertion last and removal first. It ensures that 12-volt and 3.3-volt power circuits are energized only after all signal pins are fully seated, preventing dangerous voltage spikes. It is NOT broken or damaged!

#### 2. The Eraser Rubbing Technique (The Gold Standard)
* Take a clean, soft white vinyl pencil eraser (never use abrasive pink pencil erasers or ink erasers, which strip gold plating).
* Support the underside of the PCB edge with your fingers to prevent flexing.
* Rub the eraser firmly across the gold pins on both sides in **one direction** (sweeping toward the outer tip of the teeth).
* You will see dark oxidation film and grime lift off onto the eraser rubber, leaving the gold contacts mirror-bright and reflective.

#### 3. Clean All Rubber Shavings with 90% or Higher IPA
* Thoroughly wipe both sides of the gold teeth with a lint-free microfiber cloth or cotton swab dampened with **90% or higher Isopropyl Alcohol**.
* Ensure zero rubber shavings, dust, or skin oils remain between the tiny pin gaps.
* Allow 1 to 2 minutes for the alcohol to completely evaporate.

#### 4. Motherboard PCIe Slot Cleaning
* Over months of use, dust settles inside the narrow motherboard PCIe slot, causing high-resistance contact faults.
* Use a can of compressed air at a 45° angle to blow dust and lint out of the PCIe slot.
* *Stubborn Slot Tarnish Fix:* If the slot is severely oxidized, moisten the edge of a clean piece of stiff paper or cardstock with 99% IPA, insert and slide it gently through the slot 2–3 times to scrub the internal contact springs, then blow dry.

---

### Reinstallation & Verification:
1. Align the GPU squarely over the primary PCIe x16 slot (top slot closest to the CPU).
2. Press down firmly with even pressure until you hear the plastic retention latch snap shut with a crisp click.
3. Fasten the bracket screws securely to the case to prevent GPU sag and slot strain.
4. Reconnect PCIe power cables firmly until the plastic clip latches.
5. **Verify Full Speed in GPU-Z:**
   * Boot into Windows and open **GPU-Z**.
   * Look at the **Bus Interface** box. Click the small **`?`** icon next to it and start the render test.
   * Verify that the link negotiates at full bandwidth: **`PCIe x16 4.0 @ x16 4.0`** (or `x16 3.0 @ x16 3.0`). If it still reads `x1` or `x4`, re-seat the card firmly.

---

## 4. Dust Removal & Preventive Maintenance

* **Frequency:** Clean PC interiors every 3 to 6 months depending on room environment.
* **Fan Blades:** When blowing dust off fans with compressed air, hold the fan blades in place so they do not over-spin and damage the bearings or generate reverse electrical current.
* **Thermal Paste:** Consider repasting the CPU and GPU every 2 to 3 years if temperatures begin rising under identical workloads.

---

## 5. Motherboard Stuck on Brand / Splash Logo: CMOS Reset Fix

### Symptoms:
* PC powers on (fans, LEDs, and RGB turn on), but the display stays **permanently frozen on the motherboard manufacturer splash screen** (ASUS, MSI, Gigabyte, ASRock, Dell, HP, Lenovo).
* Pressing `Del`, `F2`, or `F12` does not enter BIOS or the boot menu.
* The system hangs indefinitely during early device enumeration, USB peripheral handshakes, or after an improper shutdown.

### Why This Happens:
Corrupted BIOS NVRAM settings, bad memory training profiles, conflicting PCIe/USB hardware states, or residual capacitive charge holding the motherboard chipset in an unresponsive state.

### The Fix: Cold CMOS Battery Reset (Step-by-Step):
1. **Power Off & Unplug:** Switch off the power supply toggle switch (`O`) and disconnect the main AC power cord completely from the wall.
2. **Discharge Residual Capacitors:** Press and hold the PC case power button for **15 to 20 seconds**. This completely drains residual electricity stored in motherboard and PSU capacitors.
3. **Locate the CMOS Coin Cell Battery:**
   - Look for the round, silver **CR2032 3V coin cell battery** on the motherboard (commonly found between PCIe slots or tucked beneath the graphics card).
   - If blocked by a large graphics card, release the PCIe retention latch and remove the GPU.
4. **Remove the Battery:**
   - Gently press the small metal retention clip on the side of the battery socket using a fingernail or non-conductive plastic tool.
   - The battery will pop up at an angle. Lift it out.
5. **Drain Residual Power & Wait (The Fast Reset Trick):**
   - **Fast Reset (Recommended):** While the battery is removed, press and hold the PC case power button for **10 to 15 seconds** (or press it several times). This forces any remaining charge in the motherboard circuitry to drain immediately, clearing the NVRAM state in seconds without waiting.
   - Alternatively, leave the battery out for **1 to 5 minutes** to let residual charge decay naturally.
   - *(Jumper Shortcut: If your motherboard has a `CLR_CMOS` or `JBAT1` 2-pin header, you can also bridge both pins with a metal screwdriver tip for 5–10 seconds while the battery is removed to short the CMOS memory circuit to ground).*
6. **Reinstall & Boot:**
   - Reinsert the CR2032 battery with the smooth positive (**`+`**) terminal side (+3V) facing upward until it clicks into place.
   - Reinstall the GPU (if removed), reconnect the power cord, and power on the PC.
7. **Expected Behavior:**
   - The PC may power cycle once or twice as it relearns hardware and completes fresh memory training.
   - The freeze will clear, and the motherboard will either boot directly to Windows or display: *"Press F1 to enter setup / restore default settings"*. Enter BIOS, re-enable XMP/EXPO, set system time/boot drive, and save.
