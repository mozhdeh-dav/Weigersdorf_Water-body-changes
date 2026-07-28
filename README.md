# Pond and Lake Change Near Weigersdorf, Saxony (1930–Today)

A historical GIS analysis comparing small water bodies (ponds and lakes) visible on a 1930 topographic survey with their present-day condition, using manual digitizing, georeferencing, and spatial classification in QGIS.

![Map preview](map/weigersdorf_lake_change_map.png)

## Overview

This project digitizes water bodies from a historic Prussian *Messtischblatt* (1:25,000 topographic sheet) covering the area around Weigersdorf, Saxony, and compares them against present-day satellite/aerial basemap imagery. Each digitized feature is classified as **Persisting**, **Changed**, **Lost**, or **New**, allowing the extent of landscape change over roughly 95 years to be quantified and mapped.

## Data Sources

1. **Historic map:** *Weigersdorf.* Messtischblatt 4753 (2752/39), 1:25,000. Surveyed 1900/01, published 1906, revised 1923, Prussian part revised 1930. Sächsische Landesbibliothek – Staats- und Universitätsbibliothek Dresden (SLUB), Kartensammlung, Signatur SLUB/KS 17967. Accessed via the [Virtuelles Kartenforum](https://kartenforum.slub-dresden.de/en/) / Deutsche Fotothek, SLUB Dresden.
2. **Modern basemap:** [fill in — e.g. CartoDB Positron / OpenStreetMap contributors]
3. **Software:** [QGIS](https://qgis.org), QGIS Development Team / QGIS Association.

## Methodology

1. **Georeferencing** — The scanned historic sheet was georeferenced in QGIS using the Georeferencer tool, with control points placed on stable long-term features (church towers, road intersections). Target CRS: ETRS89 / UTM zone 33N (EPSG:25833). A polynomial (affine) transformation was used; GCP residuals were reviewed and outlier points corrected.
2. **Digitizing** — Water body outlines visible on the georeferenced historic sheet were manually digitized as polygons.
3. **Classification** — Each digitized polygon was compared against present-day basemap imagery and assigned a `status` attribute:
   - `Persisting` — present and largely unchanged in shape/extent
   - `Changed` — present today but with a measurable change in shape or size
   - `Lost` — visible in 1930, no corresponding water body today
   - `New` — present today, not visible on the 1930 sheet
4. **Area calculation** — Polygon areas were calculated in QGIS (ellipsoidal area, GRS80) and summarized by category using the *Statistics by Categories* tool to compute the share of total historic pond area in each class.

## Results

| Category | Share of total mapped pond area |
|---|---|
| Persisting | 58.4% |
| Changed | 22.5% |
| Lost | 13.6% |
| New | 5.5% |

Of the 41 ponds and lakes digitized from the 1930 sheet, the majority remain recognizable today, but a meaningful share — concentrated in a cluster in the northeastern part of the mapped area — has disappeared entirely. A smaller number of new ponds have appeared since 1930, not present on the original survey.

## Discussion

This pattern is broadly consistent with documented land-use trends across similar glacial moraine landscapes in northeastern Germany, where small kettle-hole ponds (*Sölle*) were often drained during 20th-century agricultural intensification to consolidate farmland into larger, machine-workable plots. Without additional local records, this cannot be confirmed as the specific cause at Weigersdorf, but the clustering and small size of the lost ponds are consistent with this broader regional process.

## Limitations

- Positional accuracy is limited by the precision of the original 1930 survey and by residual georeferencing error.
- Percentages are area-based rather than count-based, to better reflect the true extent of change, since pond size varied considerably across the study area.
- Classification (`Persisting` / `Changed` / `Lost` / `New`) was determined by visual comparison and may be subject to interpretation, particularly for small or ambiguous features.

## Repository Contents

```
├── data/
│   ├── weigersdorf_1930_georeferenced.tif   # Georeferenced historic map scan
│   └── lakes.gpkg                           # Digitized water body polygons with status attribute
├── map/
│   └── weigersdorf_lake_change_map.png      # Final layout export
└── README.md
```

## Tools

- [QGIS](https://qgis.org) — georeferencing, digitizing, spatial analysis, and layout
- [SLUB Dresden Virtuelles Kartenforum](https://kartenforum.slub-dresden.de/en/) — historic map source

## License / Attribution

Historic map scan © SLUB Dresden, used under [applicable open access terms — confirm before publishing]. Modern basemap © respective provider (see Data Sources above). This project's original digitized data and analysis are shared under [choose a license, e.g. CC BY 4.0].
