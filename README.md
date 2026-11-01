# SLID 1.7.104 Compatibility 0.0.1

Replacement DLL for **SLID Main 1.4.9** on **Steam Skyrim 1.7.104.0 only**.
Original SLID by **ohfor**: https://www.nexusmods.com/skyrimspecialedition/mods/172801
Upstream source: https://github.com/ohfor/slid
Nexus binary download: https://www.nexusmods.com/skyrimspecialedition/mods/195830?tab=files

This repository hosts corresponding source code, dependency sources/licenses,
build instructions and audit information. Get the installable binary from Nexus.

## Requirements and installation

- Original SLID **Main 1.4.9** and its requirements (including SkyUI).
- SKSE64 **2.3.1 or later compatible with runtime 1.7.104.0**.
- Address Library data matching **1.7.104.0** (format 5).
- SLID Babel 1.4.9 is optional. **SCIE is not required.**

Install the original SLID first, then this compatibility ZIP as a separate mod.
In MO2's left pane, place this patch below SLID (and Babel, if installed).
Let it overwrite **SKSE/Plugins/SLID.dll**. Keep the original **SLID.esp** enabled.
There is no additional ESP and no new load-order rule for other plugins.
This is a runtime port, not an SCIE-to-SLID integration patch; upstream's optional
SCIE integration remains available.

## Validation

The user reported completing the following manual tests on 2026-11-01,
Steam Skyrim 1.7.104.0 / SKSE 2.3.1, without problems:

- Game launch and SLID configuration UI.
- Creating a Link and registering persistent test containers.
- Filter-based item distribution and checking resulting item counts.
- Saving, quitting the game, and reloading the test save.

The subsequent log shows ActivateRef installed, SLID loaded successfully,
and the TEST network restored. Offline checks cover AMD64 exports, format-5
metadata, 81 preserved Papyrus registration names and five rejection cases.
These tests do not establish exhaustive compatibility or long-term save safety.
Vendor selling, restock, all UI paths and full SCIE crafting consumption have
not been confirmed by these tests.

The release DLL is byte-for-byte identical to the tested trial build:
SHA-256 `6e05061237d7557704132343cf0e9430353dbc8d77126c5d98d28f9db23f2c2a`.
Its diagnostic log still says "compatibility trial 0.0.1"; no code was changed
after the successful user test.

## Filter priority with crafting overhauls

SLID's Crafting Materials filter includes items usable as smelter inputs.
CCOR can therefore make a weapon such as an iron dagger match that category.
If weapons should remain in weapon storage, place **Weapons above Crafting
Materials** in Configure. Higher-priority filters claim matching items first.
This is upstream filter behavior, not a change made by this port.

## Port changes and limits

- Rebuild with the locally ported CommonLibSSE-NG and format-5 Address Library.
- Restrict loader metadata and entry guard to Steam 1.7.104.0 / SKSE 2.3.1+.
- Adapt message-box, HUD notification, character input and topic-event APIs.
- Check the audited activation-function entry before installing the hook.
  If another DLL has already changed those bytes, the port fails closed and
  reports a load failure rather than hooking an unverified entry.
- Lock the quest alias map while updating the vendor reference.
- No original ESP, PEX, SWF, translations, INIs, gameplay balance or SCIE files
  are changed or bundled in the Nexus patch.

Build instructions: [BUILD.md](BUILD.md). Source changes: [SLID-compatibility.patch](SLID-compatibility.patch).
Upstream revision: `c630dba767fd5d0cadb7903d3fa08e377deb86ef` (1.4.9).
All upstream and dependency notices are retained under their respective licenses;
see SLID/LICENSE and Licenses/. The bundled CommonLib has its own license and exceptions.
