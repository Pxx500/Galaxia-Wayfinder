---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Germanium Acquisition And Early Orbital Availability Research

Source: Immutable GTNH 2.8.0 baseline source inspection in GT5-Unofficial, NewHorizonsCoreMod, and GT-New-Horizons-Modpack
Imported: 2026-09-17

## Source Snapshot

### Conclusion

Germanium exists and has survival acquisition routes. The clearest verified route is IV-era Sphalerite roasting in the Alloy Blast Smelter. No HV or early pre-Luna bootstrap was verified. This is not a proof that every exotic recycling, reward, or cross-mod route is impossible.

The blocking condition in the verified normal route is machinery and power, not a requirement that Sphalerite must be mined in space. Sphalerite is explicitly present in Nether sulfur veins. The Alloy Blast Smelter requires an IV machine in both checked controller recipes and enforces recipe voltage tier against input-hatch voltage tier.

This evidence does not establish the earliest possible player route to all IV infrastructure or prove that visiting Luna is mandatory. It establishes that a proposed HV-era orbital SiGe chain cannot assume this normal Germanium route is already available.

### Revisions And Method

All recipe and progression claims below use immutable `git show` at the supplied baseline revisions:

- GT5-Unofficial: `000a4d9b24d77f40a79da7a105bb79ac7efca817`
- NewHorizonsCoreMod: `fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af`
- GT-New-Horizons-Modpack, including quests: `c3ba07ccba1b772777f6fc57e53bb70c8547adb7`

Current-code graph discovery was used to locate material owners, followed by pinned source inspection. Current checkout HEADs differ: GT5 `200352fef4bf48893e1d7c06bd66381e5cf56d70`, CoreMod `38b12ce3d59f8061742e47a63c6f1f29b7959313`, and modpack `965462fb102acf429818c07388bdf5f50137c662`. Current definitions were not substituted for pinned recipes. No branches were checked out, no code was edited, and no builds or runtime recipe tests were run.

### Definition Is Not Acquisition

GT++ defines Germanium as a solid elemental material, symbol `Ge`, and generates its material forms. This proves registration, not progression access. See [MaterialsElements.java, lines 57–68](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtPlusPlus/core/material/MaterialsElements.java#L57-L68) and [ModItems.java, line 257](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtPlusPlus/core/item/ModItems.java#L257).

### Verified Acquisition Routes

| Route | Inputs | Machine and recipe voltage | Germanium result and constraints |
| --- | --- | --- | --- |
| Sphalerite roasting | 1 purified crushed Sphalerite, 4 Carbon dust, 250 mB Sulfuric Acid, integrated circuit 15 | Alloy Blast Smelter, 4000 EU/t, 750 ticks | 36 mB Germanium fluid, one quarter ingot. Recipe is in the IV voltage band and the machine explicitly checks hatch tier |
| Sphalerite flotation | 256 milled Sphalerite, 32 Sodium Ethyl Xanthate, 14000 mB Pine Oil | Flotation Cell, `RECIPE_LuV`, 8 minutes | Produces 1000 mB Sphalerite froth per operation, not Germanium yet |
| Froth separation | 4000 mB Sphalerite froth, circuit 1 | Vacuum Furnace recipe map, `RECIPE_LuV`, 5500 K coil requirement, 2 minutes | 15 Germanium dust, 180 Zinc dust, 120 Iron dust, 64 Indium dust, plus water and red mud |
| CoreMod bee-assisted froth separation | Same 4000 mB froth plus 256 Indium combs, circuit 2 | Vacuum Furnace recipe map, `RECIPE_LuV`, 5500 K, 2 minutes | Same 15 Germanium dust, with higher Indium output. Does not lower the Germanium progression gate |

Pinned sources:

- [Sphalerite roasting, RecipesGregTech.java, lines 860–870](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtPlusPlus/core/recipe/RecipesGregTech.java#L860-L870)
- [Flotation, RecipeLoaderMilling.java, lines 235–248](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtPlusPlus/core/item/chemistry/RecipeLoaderMilling.java#L235-L248)
- [Froth separation, RecipeLoaderMilling.java, lines 41–57](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtPlusPlus/core/item/chemistry/RecipeLoaderMilling.java#L41-L57)
- [Milled Sphalerite generation uses LuV, ModItems.java, lines 938–939](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtPlusPlus/core/item/ModItems.java#L938-L939)
- [Bee-assisted recipe, CoreMod VacuumFurnaceRecipes.java, lines 28–48](https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/VacuumFurnaceRecipes.java#L28-L48)

### Why Roasting Is Not An HV Bootstrap

The pinned shaped Alloy Blast Smelter controller recipe includes an IV Alloy Smelter, elite circuits, Zirconium Carbide plates, and tiered cable. The alternative CoreMod assembler recipe runs at EV but still consumes an IV Alloy Smelter and IV circuits, plus Tungsten cable and Zirconium Carbide plates. The EV assembly voltage therefore does not make the controller an EV or HV progression item. See [RecipesMachines.java, lines 1691–1702](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtPlusPlus/core/recipe/RecipesMachines.java#L1691-L1702) and [CoreMod AssemblerRecipes.java, lines 3295–3303](https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/AssemblerRecipes.java#L3295-L3303).

The ABS checks `getTier(getAverageInputVoltage())` against `getTier(recipe.mEUt)` and rejects insufficient voltage. More low-tier amperage is not a demonstrated bypass. See [MTEAlloyBlastSmelter.java, lines 198–207](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtPlusPlus/xmod/gregtech/common/tileentities/machines/multi/production/MTEAlloyBlastSmelter.java#L198-L207).

Pinned quest guidance also calls the ABS IV and places its materials in the IV multiblock stage. See [Industrial Coke Oven quest, line 15](https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/MultipleQuestLine/IndustrialCokeOv-AAAAAAAAAAAAAAAAAAAMOQ%3D%3D.json#L15).

Sphalerite ore itself does not force a Moon trip. It is the sporadic ore in the Sulfur vein enabled in the Nether, as well as listed space bodies. See [OreMixes.java, lines 138–149](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/api/enums/OreMixes.java#L138-L149). Its ordinary GT byproducts are Yellow Garnet, Cadmium, Gallium, and Zinc, not Germanium. See [Materials.java, line 1763](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/api/enums/Materials.java#L1763). The custom roasting and flotation recipes are separate recovery routes. A full Carbon, acid, ore-washing, IV infrastructure, and travel dependency proof was not performed.

### Alburnite And Generated Processing

Alburnite is a genuine alternative, not just a material name. It is defined with Gold, Germanium, Tellurium, and Sulfur components in the ratio 8:1:2:4. Its comments contain inconsistent formulas, so the component list is the evidence used here. See [MaterialsOres.java, lines 81–97](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtPlusPlus/core/material/MaterialsOres.java#L81-L97).

The Everglades loader generates Alburnite ore and processing forms. `MaterialGenerator` attaches `RecipeGenOre`. Its default enables component decomposition, with up to six components sent to the electrolyzer. Thus Alburnite dust has a source-backed generated decomposition route to Germanium dust. The generator also provides component-based ore-processing bonus outputs. See [GTPPEverglades.java, line 113](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/toxiceverglades/GTPPEverglades.java#L113), [MaterialGenerator.java, lines 328–359](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtPlusPlus/core/material/MaterialGenerator.java#L328-L359), and [RecipeGenOre.java, lines 382–489](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtPlusPlus/xmod/gregtech/loaders/RecipeGenOre.java#L382-L489).

The generated Alburnite electrolyzer voltage is source-derived as 16 EU/t. Alburnite passes melting-point argument -1, the material constructor derives `vTier` from that argument, and the tier-to-voltage helper maps tier 0 to 16. This is a code derivation, not a runtime recipe dump. See [Material.java, lines 562–567](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtPlusPlus/core/material/Material.java#L562-L567) and [MaterialUtils.java, lines 202–216](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtPlusPlus/core/util/minecraft/MaterialUtils.java#L202-L216). Low separation voltage does not prove early acquisition of Alburnite.

Verified Alburnite supply paths have later gates:

- **Rare Earth (III):** 3 Rare Earth dust plus 1000 mB GT++ Hydrofluoric Acid, or 2000 mB GT Hydrofluoric Acid, goes through an IV chemical bath to Rare Earth (III) crushed material. Its composition includes Alburnite. Generated dehydration operates at its explicitly assigned IV tier, 7680 EU/t, and separates its component dusts including Alburnite. These are source-derived generated steps, not a runtime dump. See [RecipesRareEarthProcessing.java, lines 100–125 and 159–176](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtPlusPlus/core/recipe/RecipesRareEarthProcessing.java#L100-L176), [MaterialMisc.java, lines 228–243](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtPlusPlus/core/material/MaterialMisc.java#L228-L243), and [RecipeGenOre.java, lines 493–605](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtPlusPlus/xmod/gregtech/loaders/RecipeGenOre.java#L493-L605).
- **Toxic Everglades mining:** Alburnite appears in ore vein 12. Portal-frame assembly is LuV and uses higher-tier components. The activation disk needs an IV laser engraving recipe. The pinned quest places normal access in ZPM. This is not an HV shortcut just because the final ore separation is cheap. See [WorldGenEvergladesOres.java, lines 152–162](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/toxiceverglades/gen/WorldGenEvergladesOres.java#L152-L162), [RecipesMachines.java, lines 2909–2923](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtPlusPlus/core/recipe/RecipesMachines.java#L2909-L2923), and [RecipesLaserEngraver.java, lines 119–125](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtPlusPlus/core/recipe/RecipesLaserEngraver.java#L119-L125).
- **Space mining:** The Everglades asteroid output table contains Alburnite ore. Its base recipe is IV, but it explicitly uses ZPM through UHV drone tiers. The recipe's IV EU label is not proof of IV or pre-Luna access to the full orbital miner system. See [SpaceMiningRecipes.java, lines 532–553](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtnhintergalactic/recipe/SpaceMiningRecipes.java#L532-L553).

### Limits And Planning Relevance

No dedicated early Germanium ore, small-ore, or ordinary Sphalerite byproduct shortcut was verified in the inspected registrations and pinned sources. This is a bounded finding, not an absence proof. Generated Alburnite processing was explicitly checked rather than treating a text-search miss as unavailability. High-tier recycling, Godforge conversions, arbitrary rewards, and every cross-mod ore source were not audited. No claim is made that any space trip is universally mandatory.

The defensible planning statement is: **Germanium is an existing GTNH material with verified IV-era acquisition and later alternatives. An HV or early pre-Luna SiGe bootstrap is not currently evidenced and should remain conditional.** No replacement material, custom recipe, or progression change is selected by this note.

[[Sources]]
