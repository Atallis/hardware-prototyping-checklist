# Hardware Prototyping Checklist

A no-BS, phase-by-phase checklist for teams building hardware prototypes — from first idea to production handoff.

## Why This Exists

I'm Julien, an electronics engineer based in Montreal. I run [Atallis Solutions](https://atallis.com), a hardware prototyping studio. Over the past few years I've helped startups, creative agencies, and R&D teams take hardware ideas from napkin sketch to working product — IoT sensors for industrial equipment, custom LED displays, BLE controllers, stereo camera systems, interactive installations, and more.

Every one of these projects taught me something. Usually the hard way. And I loved every minute of it — even the painful debugging sessions at 11pm with an oscilloscope and a puzzled face.

The pattern I kept seeing: **teams don't fail because of bad engineering — they fail because they skip steps.** They jump straight to PCB layout because it feels productive, skip the architecture phase because "we already know what we're building," or order boards before validating the risky parts on a breadboard. Then they spend 3x the time fixing what should have been caught early.

This checklist is what I wish someone had handed me on my first project. It's the same process I now follow with every client, whether it's a startup building their first IoT device or a design studio adding electronics to a physical product for the first time.

**It's opinionated.** It reflects how I work and what I've seen go wrong. Your mileage may vary, but if you're building hardware and don't have a process yet — this is a solid starting point.

I also share this with every client at the start of a project. Hardware development can feel like a black box when you're a founder or a creative director working with an engineer for the first time. This checklist makes the process transparent — you always know what phase we're in, what's been validated, and what's coming next. No surprises, no "trust me, it's almost done."

---

## Who This Is For

- **Hardware startups** building their first prototype (this is most of my clients — and the ones who benefit most from a structured process)
- **Creative agencies & design studios** adding electronics to physical products (you have the design chops, you just need the electronics roadmap)
- **Founders working with a hardware engineer** who want to understand what's happening and why (this checklist is your window into the process)
- **R&D teams** exploring new product lines
- **Makers** ready to graduate from breadboard to a real product

---

## How to Use This Checklist

**If you're building it yourself:** Work through each phase in order. Check items off as you go. Not every item applies to every project — use judgment. But skipping a *phase* entirely is almost always a mistake.

**If you're working with an engineer (or with us):** Use this as a shared reference. Ask "what phase are we in?" at any point. If your engineer can't answer clearly, that's a red flag. A good hardware process has clear gates between phases — you validate before you commit.

The phases are sequential. I know Phase 4 (PCB layout) is the fun part. Resist the urge to jump there before the architecture is solid — it will save you a respin and a few hundred dollars in wasted PCBs.

> **Tip:** Fork this repo and check items off as you go, or copy it into whatever project management tool you use.

---

## Phase 0 — Define the Problem

Before touching any hardware, make sure you're solving the right problem. I've had clients come in saying "I need a custom PCB" when what they actually needed was a $12 dev board and three lines of code. This phase prevents you from building the wrong thing really well.

- [ ] **Problem statement written down** — one sentence describing what this device does and why it matters
- [ ] **Target user identified** — who will use this and in what context?
- [ ] **Success criteria defined** — what does "working" look like? Be specific (e.g., "reads temperature within +/-0.5C and transmits via BLE every 10 seconds")
- [ ] **Form factor constraints listed** — max dimensions, weight, enclosure requirements
- [ ] **Environment defined** — indoor/outdoor, temperature range, IP rating needed, vibration, humidity
- [ ] **Power budget estimated** — battery life target, available power sources, charging method
- [ ] **Connectivity requirements listed** — Wi-Fi, BLE, LoRa, cellular, USB, Ethernet, none
- [ ] **Regulatory landscape identified** — FCC, CE, IC, UL — which certifications are needed?
- [ ] **Budget and timeline documented** — how much money and time do you have?
- [ ] **Existing solutions reviewed** — what's already on the market? Why build custom?

---

## Phase 1 — System Architecture

The most important phase, and the one most teams rush through. I cannot overstate this: **a bad architecture will haunt you for the entire project.** I've seen teams spend months debugging problems that were baked into their block diagram on day one.

On one of my IoT projects — an industrial vibration monitoring system — we spent a full week just on architecture before touching a single component. MCU selection, power rail design, communication strategy, sensor placement. The result? First prototype worked on power-up, and we went from first conversation to field-deployed hardware in six weeks. That doesn't happen by accident.

- [ ] **Block diagram created** — every major subsystem as a box, arrows showing data/power flow
- [ ] **Microcontroller / processor selected** — based on actual requirements, not familiarity
  - [ ] GPIO count sufficient?
  - [ ] Peripherals needed are available (SPI, I2C, UART, ADC, PWM)?
  - [ ] Processing power adequate for the application?
  - [ ] Power consumption fits the budget?
  - [ ] Sufficient flash and RAM?
  - [ ] Toolchain and SDK quality evaluated?
  - [ ] Supply chain availability checked (stock, lead times, second sources)?
- [ ] **Sensors / actuators selected** — datasheets reviewed, not just marketing specs
- [ ] **Communication protocol chosen** — wired (I2C, SPI, UART, CAN) and wireless (BLE, Wi-Fi, LoRa)
- [ ] **Power architecture designed**
  - [ ] Input voltage(s) identified
  - [ ] Voltage rails listed with current estimates
  - [ ] Regulator topology chosen (LDO vs. switching, efficiency targets)
  - [ ] Battery chemistry selected (if applicable)
  - [ ] Charging circuit defined (if applicable)
  - [ ] Power sequencing requirements identified
- [ ] **Interface / connectors chosen** — USB-C, JST, headers, pogo pins, etc.
- [ ] **Critical components evaluated for availability** — check stock on Mouser/Digi-Key before committing
- [ ] **Bill of Materials (BOM) draft started** — even rough, it forces discipline
- [ ] **Make-vs-buy decisions documented** — which subsystems are custom, which are modules?
- [ ] **Architecture review done** — someone other than the designer reviews the block diagram

---

## Phase 2 — Proof of Concept (Breadboard / DevKit)

Validate the risky parts before committing to a PCB. This is the cheapest phase to fail in — a breadboard costs nothing, a bad PCB costs time and money. I tell every client: if we're going to discover a showstopper, let's discover it now, with jumper wires, not after we've ordered 50 boards.

- [ ] **Dev kit or eval board acquired** for the main MCU
- [ ] **Critical subsystems validated individually**
  - [ ] Sensor reads correctly?
  - [ ] Actuator responds as expected?
  - [ ] Communication link established (BLE advertising, Wi-Fi connection, etc.)?
  - [ ] Power consumption measured — matches estimates?
- [ ] **End-to-end data path proven** — sensor → MCU → processing → output/transmission
- [ ] **Firmware skeleton running** — basic init, peripheral drivers, main loop structure
- [ ] **Edge cases tested** — what happens at power boundaries, signal limits, temperature extremes?
- [ ] **Risk register updated** — what unknowns remain? What could still fail?
- [ ] **Go/no-go decision documented** — is the architecture validated enough to proceed to PCB?

---

## Phase 3 — Schematic Design

Translating the validated architecture into a proper schematic.

- [ ] **Schematic tool set up** — KiCad, Altium, etc. with project structure and libraries
- [ ] **Component symbols verified** — pin assignments match datasheets, not just random library parts
- [ ] **Power supply section complete**
  - [ ] Input protection (reverse polarity, overvoltage, ESD)
  - [ ] Regulators with proper input/output capacitors per datasheet
  - [ ] Power indicator LED(s)
  - [ ] Test points on every voltage rail
- [ ] **Decoupling capacitors placed** — per datasheet recommendations, close to IC power pins
- [ ] **Crystal / oscillator circuit correct** — load capacitors calculated, not guessed
- [ ] **Reset circuit proper** — supervisor IC or RC circuit with proper threshold
- [ ] **Programming / debug header included** — SWD, JTAG, UART for debug
- [ ] **Boot mode configuration correct** — pull-ups/pull-downs for desired boot behavior
- [ ] **ESD protection on external interfaces** — USB, connectors, anything a user touches
- [ ] **Unused pins handled** — not left floating (tied to GND or VCC per datasheet)
- [ ] **LED indicators for debug** — power, status, communication activity
- [ ] **Mounting holes added** — with proper clearance for screw heads
- [ ] **Net naming consistent and clear** — signal names that make sense 6 months from now
- [ ] **Schematic review done** — someone else reviews, or you review after a 24-hour break

---

## Phase 4 — PCB Layout

Where electrical design meets physical reality.

- [ ] **Board outline defined** — from mechanical constraints or enclosure design
- [ ] **Stackup chosen** — 2-layer or 4-layer, with impedance control if needed
- [ ] **Component placement done before routing**
  - [ ] Connectors on board edges
  - [ ] Decoupling caps next to IC power pins
  - [ ] High-speed components close together
  - [ ] Heat-generating components away from temperature-sensitive ones
  - [ ] Test points accessible
  - [ ] Programming header accessible
- [ ] **Critical traces routed first** — power, high-speed signals, analog signals
- [ ] **Ground plane continuous** — no unnecessary splits under signal traces
- [ ] **Trace widths calculated** — for current carrying capacity (use a trace width calculator)
- [ ] **Differential pairs routed correctly** — matched length, consistent spacing
- [ ] **Antenna area clear** — no copper pour under/near antenna (if applicable)
- [ ] **Thermal relief on ground pads** — for easier hand soldering
- [ ] **Silkscreen useful** — component references, pin 1 markers, board name, version, date
- [ ] **Fiducials added** — if pick-and-place assembly is planned
- [ ] **Design Rule Check (DRC) passes** — zero errors, warnings reviewed
- [ ] **Gerber files generated and visually inspected** — use a Gerber viewer, check every layer
- [ ] **Board dimensions verified against enclosure** — does it actually fit?

---

## Phase 5 — Firmware Development

Bringing the hardware to life.

- [ ] **Development environment set up** — IDE, toolchain, debugger working
- [ ] **Hardware Abstraction Layer (HAL) defined** — don't code directly to registers unless necessary
- [ ] **Peripheral drivers validated** — GPIO, SPI, I2C, UART, ADC, timers all tested individually
- [ ] **Communication stack working** — BLE, Wi-Fi, LoRa, or whatever the project needs
- [ ] **Sensor data acquisition validated** — correct values, correct units, correct sample rate
- [ ] **Power management implemented** — sleep modes, wake sources, duty cycling
- [ ] **Watchdog timer configured** — the board must recover from crashes
- [ ] **Error handling in place** — what happens when a sensor fails, a bus locks up, or memory runs out?
- [ ] **OTA update mechanism** — if applicable, build it in early, not as an afterthought
- [ ] **Logging / debug output available** — UART debug console or similar
- [ ] **Factory reset mechanism** — button combo or pin short to restore defaults
- [ ] **Version numbering in firmware** — queryable via debug console or BLE characteristic

---

## Phase 6 — Assembly & Bring-Up

The moment of truth. This is where you find out if your design actually works in the real world. I still get a rush every time I power up a new board for the first time — and I still follow the exact same bring-up sequence every time. No shortcuts here.

- [ ] **PCBs ordered** — with correct specifications (layers, thickness, finish, color)
- [ ] **Stencil ordered** — if doing reflow soldering
- [ ] **Components ordered** — complete BOM, with spares for rework (order 2-3x for passives)
- [ ] **Assembly workspace prepared** — ESD mat, good lighting, magnification, soldering equipment
- [ ] **Power-up sequence followed**
  1. Visual inspection under magnification before applying power
  2. Check for shorts between power rails and ground (multimeter continuity)
  3. Apply power with current-limited supply, watch current draw
  4. Verify all voltage rails with multimeter
  5. Connect debugger, verify MCU is alive
  6. Flash basic blink test
  7. Test peripherals one by one
- [ ] **Known-good board established** — one fully tested reference board
- [ ] **Issues documented** — every bug, every workaround, every "huh that's weird"
- [ ] **ECO (Engineering Change Order) list started** — what to fix in the next revision

---

## Phase 7 — Testing & Validation

Does it actually meet the requirements from Phase 0?

- [ ] **Functional testing** — every feature tested against success criteria
- [ ] **Power consumption measured** — idle, active, peak, sleep — compared to budget
- [ ] **Temperature testing** — does it work across the specified range?
- [ ] **Communication range tested** — BLE, Wi-Fi, LoRa at expected distances
- [ ] **ESD testing** — at least informal (touch the board after shuffling on carpet)
- [ ] **Drop / vibration testing** — if relevant to the application
- [ ] **Battery life tested** — actual measurement, not just calculation
- [ ] **Long-duration soak test** — run continuously for 48-72 hours minimum
- [ ] **Edge case testing** — power brownout, signal loss, buffer overflow, clock drift
- [ ] **User testing** — put it in someone's hands who wasn't involved in building it

---

## Phase 8 — Iteration & Rev 2

Almost no hardware project ships on Rev 1. This isn't failure — it's the process. On a custom LED display project, Rev 1 taught us things about thermal management that no simulation would have caught. Rev 2 was rock solid. If someone tells you they'll get it right on the first PCB, they either have very simple requirements or they're underestimating the problem.

- [ ] **ECO list reviewed** — prioritize fixes vs. nice-to-haves
- [ ] **Layout changes implemented** — from bring-up findings
- [ ] **BOM optimized** — cost reduction, alternate sources, obsolescence check
- [ ] **Mechanical integration validated** — fits in enclosure with all cables, connectors, buttons
- [ ] **Test jig designed** — if building more than 5 units, invest in a test fixture
- [ ] **Assembly instructions documented** — someone else should be able to build it
- [ ] **Firmware frozen for hardware validation** — don't change firmware and hardware simultaneously

---

## Phase 9 — Production Preparation

Getting ready to build more than one.

- [ ] **Design for Manufacturing (DFM) review done** — with your PCB fab and assembly house
- [ ] **BOM finalized** — approved manufacturer part numbers, no generic "100nF cap"
- [ ] **Assembly drawings created** — component placement, polarity, special instructions
- [ ] **Test procedure documented** — step-by-step, pass/fail criteria for each test
- [ ] **Certification testing planned** — FCC/CE/IC pre-scan before formal testing
- [ ] **Firmware release process defined** — version control, build artifacts, flashing procedure
- [ ] **Supply chain secured** — components ordered or quoted with lead times understood
- [ ] **Production cost calculated** — BOM + assembly + testing + packaging + margin

---

## Common Mistakes to Avoid

These aren't theoretical — I've either made them myself or watched clients make them. Some of them cost days, some cost thousands of dollars.

1. **Skipping Phase 1** — jumping to schematic without a solid architecture always costs more time than it saves
2. **Choosing components by tutorial, not by datasheet** — "I saw it on YouTube" is not a selection criteria
3. **No test points** — you will need to probe your board. Make it easy on yourself
4. **Insufficient decoupling** — follow the datasheet. Always
5. **Not checking component availability** — designing around a chip with 52-week lead time
6. **Ignoring power budgets** — "we'll optimize later" means your battery life will always be bad
7. **No programming header on the board** — every prototype needs a debug port
8. **Hand-routing everything** — use the autorouter for a first pass, then hand-optimize
9. **Not version-controlling hardware files** — your KiCad/Altium project belongs in Git
10. **Building only one unit** — always build at least 2 prototypes. One will have an assembly defect

---

## Tools We Use and Recommend

| Category | Tool | Notes |
|----------|------|-------|
| PCB Design | [KiCad](https://www.kicad.org/) | Free, open-source, professional-grade |
| Firmware | [PlatformIO](https://platformio.org/) | Multi-platform embedded development |
| 3D / Enclosure | [Fusion 360](https://www.autodesk.com/products/fusion-360) | Integrated MCAD + ECAD |
| Version Control | [Git](https://git-scm.com/) | Yes, for hardware files too |
| BOM Management | KiCad BOM + spreadsheet | Keep it simple early on |
| PCB Fabrication | [JLCPCB](https://jlcpcb.com/) / [PCBWay](https://www.pcbway.com/) | Fast, affordable prototyping |
| Component Sourcing | [Mouser](https://www.mouser.com/) / [Digi-Key](https://www.digikey.com/) | Authorized distributors only |

---

## Contributing

Found something missing? Disagree with a recommendation? Open an issue or submit a pull request. This checklist is a living document and benefits from diverse hardware engineering experience.

---

## About

I'm Julien, founder of [Atallis Solutions](https://atallis.com) in Montreal. I help teams who have ambitious hardware ideas but need an experienced engineer to actually build them — the kind of projects where the architecture decisions on day one determine whether you ship on time or burn through three respins.

Honestly, I just love building things. There's something about seeing a board power up for the first time, watching an LED blink, getting sensor data streaming across a terminal — that never gets old. I started this company because I wanted to spend my days doing exactly this, and helping others do it well.

My clients range from IoT startups building their first connected device to creative agencies who just landed a project that needs custom electronics and have no idea where to start. In both cases, the process is the same — and this checklist is how I keep it structured.

If you're working on a hardware project and want to talk through your architecture, feel free to reach out.

**Website:** [atallis.com](https://atallis.com)
**LinkedIn:** [Atallis Solutions](https://linkedin.com/company/atallis)

---

## License

This work is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). You're free to use, adapt, and share it — just credit Atallis Solutions.
