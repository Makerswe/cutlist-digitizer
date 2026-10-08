# Cutlist Digitizer

A single-file web app that turns photos of handwritten cutting lists into the 22-column beam-saw import format (CSV / XLSX).

## What it does
- Upload one or more photos of a cutting list.
- Claude reads the photo and extracts every part (name, length, width, quantity, material, edging).
- Board codes are standardised as `MATERIAL-THICKNESS-SIZE` (e.g. `MDF-16-9X6`, `W/CM-16-9X6`).
- Parts that cannot fit on the sheet are flagged red. Sheet sizes: 8X4 = 2400x1200, 9X6 = 2740x1830, 12X6 = 3660x1830 mm.
- Order number = Job Code + space + job title (e.g. `0113 V+A WOOLWORTHS COFFEE BAR`).
- Export as semicolon CSV or XLSX in the beam-saw column order.

## Output columns
RouteCard/PartName; CatalogNum(material); PartCutLength; PartCutWidth; PartAmount; BoardThickness; SubstType; PartOverCut; PartUnderCut; LengthEdge1; Lengthedge2; Widthedge1; WidthEdge2; ModuleClient; ModuleInfo2; ModuleCatalog; ModuleOrderNum; ExtraLength; ExtraWidth; PartName; Up_Side_CNC_File_Name; Down_Side_CNC_File_Name

## Edge shorthand
EAR = all four sides. E1L / E2L = length edges 1 / 2. E1S / E2S = width edges 1 / 2.

## How to use
Open `cutlist-digitizer.html` inside Claude (as an artifact) and upload photos.

## Important: running outside Claude
The extraction call to `https://api.anthropic.com/v1/messages` sends no API key, so it works only where Claude supplies authentication. On GitHub Pages or a local file it returns HTTP 401. To run it standalone, add your own key through a small backend proxy. Never put a key in the HTML, because anyone can read it.

## Always check
Flagged numbers and red "does not fit" rows need a human check against the original photo.
