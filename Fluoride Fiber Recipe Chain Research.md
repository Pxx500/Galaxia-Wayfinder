---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Fluoride Fiber Recipe Chain Research

Source: Delegated local-source audit for the early orbital electronics and satellite chain
Imported: 2026-10-07

## Source Snapshot

This is an unaccepted recipe proposal, not an implementation plan or accepted chemistry. The owner requires specialty fluoride optical fibers in Alpha functional satellites. They are not mandatory in the first Rocket control-electronics upgrade. Their production requires microgravity. Final satellite assembly does not.

### Recommendation

Use a clearly fictional **specialty sodium-aluminium oxyfluoride glass** for the early chain, made from existing sodium fluoride, aluminium fluoride and silicon dioxide. Do not call it ZBLAN or claim real-world ZBLAN performance. This keeps two new items and no new fluids. Existing GT recipe maps can perform all operations. The environmental requirement needs Galaxia integration into the recipe-processing check, not a new machine.

Exact ZBLAN remains a later formulation candidate. Lanthanum is not established as an obtainable HV feedstock. Creating early lanthanum access would broaden this chain into rare-earth progression. Zirconium is surprisingly not itself an EV blocker because GT++ already has an HV tin-to-zirconium route.

### Baseline and citation convention

Verified exact source at GT5-Unofficial `000a4d9b24d77f40a79da7a105bb79ac7efca817` and NewHorizonsCoreMod `fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af`, using `git show`. Current checkout HEADs differ, so all numbers below refer to the requested 2.8 baseline. Source references G and C point to immutable source revisions. No game runtime was launched.

- G = https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/
- C = https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/

### Existing finite feedstock recipes

Amounts are GT recipe units, not literal real-world stoichiometric mass. Circuits and shaping dies are reusable unless stated. Cells are returned or become filled cells.

| Step | Inputs | Outputs | Machine, power, duration | Exact source |
| --- | --- | --- | --- | --- |
| Fluorine | 20 lepidolite dust + 4 empty cells | 2000 L fluorine + 1 potassium dust + 3 lithium dust + 10 aluminium oxide dust + 4 oxygen cells | Electrolyzer, MV 120 EU/t, 13 s | C `ElectrolyzerRecipes.java:267-279` |
| HF | 1 hydrogen cell + 1000 L fluorine + circuit 1 | 1000 L GT5U hydrofluoric acid + 1 empty cell | Chemical Reactor, LV 8 EU/t, 3 s | G `gregtech/loaders/postload/recipes/ChemicalRecipes.java:2298-2305` |
| Salt water | 2 salt dust + 1000 L water + circuit 3 | 1000 L salt water | Mixer, LV 8 EU/t, 5 s | G `gregtech/loaders/postload/recipes/MixerRecipes.java:1284-1292` |
| Sodium hydroxide | 1000 L salt water + 1 empty cell + circuit 1 | 3 sodium hydroxide dust + 1 hydrogen cell + 1000 L chlorine | Electrolyzer, LV 30 EU/t, 36 s | G `gregtech/loaders/postload/recipes/ElectrolyzerRecipes.java:235-244` |
| Sodium fluoride | 3 sodium hydroxide dust + 1000 L GT5U HF + circuit 15 | 2 sodium fluoride dust + 1000 L water | Chemical Reactor, LV 30 EU/t, 60 s | G `gtPlusPlus/xmod/gregtech/loaders/recipe/RecipeLoaderNuclear.java:237-244` |
| Silicon tetrafluoride | 3 silicon dioxide dust + 4000 L GT5U HF + circuit 2 | 1000 L silicon tetrafluoride | Chemical Reactor, LV 30 EU/t, 15 s | G `gregtech/loaders/postload/recipes/ChemicalRecipes.java:915-925` |
| Aluminium fluoride | 4 aluminium dust + 3000 L silicon tetrafluoride + circuit 1 | 16 aluminium fluoride dust + 3 silicon dust | Chemical Reactor, LV 30 EU/t, 30 s | G `gregtech/loaders/postload/recipes/ChemicalRecipes.java:901-913` |

Lepidolite and salt occur together in Overworld salt veins, so fluorine does not require Everglades fluorite. Source: G `gregtech/api/enums/OreMixes.java:188-199`. Aluminium and quartz feedstocks are normal early GT inputs. Use ordinary mined silicon dioxide or quartz processing. No new acquisition route is proposed for either.

### Proposed new manufacturing recipes

| Inputs | Outputs | Machine | Tier, duration | Environment |
| --- | --- | --- | --- | --- |
| 2 existing sodium fluoride dust + 4 existing aluminium fluoride dust + 3 existing silicon dioxide dust | 9 specialty fluoride-glass preforms | Electric Blast Furnace, 1800 K | HV 480 EU/t, 120 s | Microgravity |
| 1 specialty fluoride-glass preform + reusable wire extrusion die | 8 specialty fluoride optical fibers | Extruder | HV 480 EU/t, 30 s | Microgravity |

New items: `specialty_fluoride_glass_preform`, `specialty_fluoride_optical_fiber`. No blend dust, molten-glass fluid, custom die, purification quality variants or separate fiber-drawing machine. No recipe produces ordinary glass fiber or generic elemental materials from the new preform. Proposed consumer allocation: 8 fibers per functional satellite optical/sensor payload, subject to the parent chain's exact payload recipe. Final payload and satellite assembly remain unrestricted.

One preform batch yields 72 fibers. Four batches consume exactly 8 sodium fluoride dust, 16 aluminium fluoride dust and 12 silicon dioxide dust. The existing fluoride feedstock routes for this consume 16000 L HF total, 4 aluminium dust, 12 further silicon dioxide dust and 12 sodium hydroxide dust. They also return 3 silicon dust and 4000 L water. Producing that HF requires eight lepidolite electrolysis batches and sixteen HF synthesis batches. This arithmetic exposes cost for balancing without pretending it is a physical ZBLAN formula.

Existing machinery precedent: C `ExtruderRecipes.java:21-24` converts one borosilicate-glass ingot plus reusable wire die into eight glass fibers at 96 EU/t in 8 s. C `WiremillRecipes.java:34-36` provides the same yield at MV in 10 s. Choose only the Extruder path for the new fiber to avoid duplicate interchangeable recipes. These precedents establish item-in/item-out glass-fiber manufacture, not validated optical quality.

### Exact-ZBLAN input audit

**Zirconium fluoride exists**, with dust and molten-fluid forms. HV Chemical Bath: 12 tin dust + 2400 L chlorine, 30 s, gives zirconium dust rolls of 3 at 90%, 4 at 60%, 5 at 30%. LV Autoclave: 1 zirconium dust + 4000 L chlorine, 15 s, gives 1 zirconium pellet. Macerator: 1 pellet to 5 ZrCl4 dust, 2 EU/t, 20 s. EBF: 1 ZrCl4 to 1 cooked ZrCl4, 340 EU/t, 300 K, 60 s. Chemical Dehydrator: 1 cooked ZrCl4 + 800 L GT5U HF to 1 ZrF4 dust + 800 L HCl, HV, 30 s. Sources: G `RecipeLoaderNuclear.java:68-75,90-96,101-112,344-354,581-587`, under the GT++ recipe-loader path above. Do not confuse this with Lanthanides' separate EV/4500 K metal reduction or the MV RedZircon route whose ore is on Ross worlds.

**Barium dust exists**. Barite material composition enables autogenerated electrolysis, with one barium per six formula dust units, plus sulfur and oxygen. Sources: G `gregtech/loaders/materials/MaterialsInit1.java:810` and `gregtech/loaders/oreprocessing/ProcessingDust.java:155-227`. Its earliest obtainable ore source was not established in this audit. Europa dust processing produces barium at HV, but machine voltage alone does not establish early destination access. Source: C `CentrifugeRecipes.java:166-186`. No baseline barium-fluoride recipe or dedicated material was found.

**Lanthanum dust exists**, but its native ore mix is on Barnard E/F, Centauri Alpha and Vega B, not the starting world. Source: G `gregtech/api/enums/OreMixes.java:807-817`. Nano-resin recovery produces molten lanthanum at ZPM. Source: G `gtnhlanth/loader/RecipeLoader.java:2403-2413`. Haumea stone yields lanthanum with an IV centrifuge but still needs that destination. Source: C `CentrifugeRecipes.java:364-373`. The UHV QFT bastnasite shortcut is not an HV bootstrap. No baseline lanthanum-fluoride material/recipe was found. These are observed routes, not a proof that every third-party source is absent.

**Sodium fluoride and aluminium fluoride** have existing LV dust routes above. **HF** is already accessible at MV through lepidolite and LV synthesis. GT++ fluorite also supplies 16000 L HF from 37 fluorite dust + 8000 L sulfuric acid in a Chemical Dehydrator at 240 EU/t in 600 s, with calcium sulfate and chance metal byproducts. Source: G `gtPlusPlus/xmod/gregtech/loaders/RecipeGenFluorite.java:251-269`. It is a valid existing alternative, not the selected earliest bootstrap.

### Open blockers

Owner approval is needed for fictional oxyfluoride rather than exact ZBLAN. Exact ZBLAN needs early lanthanum acquisition, confirmed early barite access, and two new fluoride compounds. None is authorized by this proposal. Microgravity recipe enforcement must be supported by the shared environmental capability check. The proposed HV furnace/extruder numbers are content-design choices, not existing recipes or real optical-performance measurements.

[[Sources]]
