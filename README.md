# ArubaAirheads-PlantUML

This repository uses Aruba Networking PPT icons ([All_Aruba_PPT_Icons_4AirHeads.zip](https://community.arubanetworks.com/discussion/aruba-ppt-icons)) package from Aruba Airheads.

The following projects were used to generate the images available in this repository:

* Convert PPT to PPTX using PowerPoint, rename the exported PPTX file to ".zip" and extracted it.
* Inkscape to convert EMF to PNG.
* XnConvert to transform-rotate PNG files.
* PlantUML to convert white background PNGs to Sprites (.puml files). 

The following commands were used:

```bash
for f in *.emf; do inkscape --actions "transform-rotate:180" --export-type="png" --export-id="$(inkscape --query-all "${f}" &>/dev/null | grep -m 1 '^svg' | cut -d ',' -f 1)" $f --export-filename ${f/.emf/.png}; done
find . -name '*.png' | sed -e 's/\.png$//' | parallel "plantuml -encodesprite 16z {}.png >> ../puml/{}.puml"
```
