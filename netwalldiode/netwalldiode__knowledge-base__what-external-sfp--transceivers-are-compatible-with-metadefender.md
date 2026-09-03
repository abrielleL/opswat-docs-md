<!-- source: https://www.opswat.com/docs/netwalldiode/knowledge-base/what-external-sfp--transceivers-are-compatible-with-metadefender -->

# What external SFP+ transceivers are compatible with MetaDefender Optical Diode (NIC Intel X710-DA2)?

**Check Your Version:**

This article applies to MetaDefender Optical Diode 10 GbE Models.

## [**Purpose**](/docs/netwalldiode/knowledge-base/what-external-sfp--transceivers-are-compatible-with-metadefender#purpose)

This article lists **supported / recommended** SFP+ transceiver and cable types for the **external data ports** on MetaDefender Optical Diode appliances that ship with an **Intel X710‑DA2** network adapter.

## [**Applies to**](/docs/netwalldiode/knowledge-base/what-external-sfp--transceivers-are-compatible-with-metadefender#applies-to)

- MetaDefender Optical Diode (10 GbE models)
- Appliances configured with **Intel X710‑DA2** (dual‑port 10GbE SFP+) for external networking
- External SFP+ slots on the NIC (commonly labeled **SFP3/SFP4** or “slots 5/6” on the rear panel)

**Not in scope:** The internal BLUE→RED one‑way optical link. That link uses OPSWAT‑supplied directional optics and is not interchangeable with the transceivers below.

## [**Hardware context**](/docs/netwalldiode/knowledge-base/what-external-sfp--transceivers-are-compatible-with-metadefender#hardware-context)

- **External data NIC:** Intel **X710‑DA2** (dual SFP+ 10GbE)
- **Internal diode optics:** Directional **TX‑only / RX‑only** SFP+ modules mounted inside the chassis (used solely for the one‑way enforcement link)

## [**Recommended transceivers & cables for the X710‑DA2**](/docs/netwalldiode/knowledge-base/what-external-sfp--transceivers-are-compatible-with-metadefender#recommended-transceivers--cables-for-the-x710da2)

Use **Intel‑coded or Dell‑labeled** parts for best compatibility.

### [**1) 10GBASE‑SR (MMF, LC, 850 nm)**](/docs/netwalldiode/knowledge-base/what-external-sfp--transceivers-are-compatible-with-metadefender#1-10gbasesr-mmf-lc-850-nm)

- **Intel**: **E10GSFPSR**
- **Dell**: **SFP‑10G‑SR** (family; e.g., part 407‑BBOU)

### [**2) 10GBASE‑LR (SMF, LC, 1310 nm)**](/docs/netwalldiode/knowledge-base/what-external-sfp--transceivers-are-compatible-with-metadefender#2-10gbaselr-smf-lc-1310-nm)

- **Intel**: **E10GSFPLR**
- **Dell**: **SFP‑10G‑LR** (family; e.g., parts 407‑BBOP / 407‑BCDT)

### [**3) SFP+ Direct‑Attach Copper (Twinax DAC)**](/docs/netwalldiode/knowledge-base/what-external-sfp--transceivers-are-compatible-with-metadefender#3-sfp-directattach-copper-twinax-dac)

- **Intel/Dell** passive DAC
- **Intel/Dell** active‑limiting DAC

**Tip:** Keep NIC firmware/drivers current. If a link doesn’t come up, check module coding (Intel/Dell), link partner capability (10G SFP+), and cable/fiber polarity.

## [**Not recommended / often blocked by X710**](/docs/netwalldiode/knowledge-base/what-external-sfp--transceivers-are-compatible-with-metadefender#not-recommended--often-blocked-by-x710)

- **10GBASE‑T (RJ‑45) SFP+ copper modules** (high power; frequently unsupported/unstable on X710)
- **Generic/uncoded SR/LR optics** (may be rejected by module validation)
- **BiDi/CWDM/DWDM/FC/SAN** SFP/SFP+ modules (not validated for this NIC’s 10GbE Ethernet use case)

If **Further Assistance** is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).

MetaDefender
