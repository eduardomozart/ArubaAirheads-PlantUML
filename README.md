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

## Getting Started

### ClearPass Certificates

![Basic usage - ClearPass Certificates](https://www.plantuml.com/plantuml/proxy?idx=0&src=https%3A%2F%2Fraw.githubusercontent.com%2Feduardomozart%2FArubaAirheads-PlantUML%2Fmain%2FSamples%2FClearPass_Certs.puml)

```csharp
@startuml
scale 1/3
skinparam defaultFontName Helvetica
left to right direction

!define LyncPuml https://raw.githubusercontent.com/eduardomozart/LyncServer2010-PlantUML/main
!include LyncPuml/LyncServer2010VisioStencil/puml/Certificate.puml

!define ArubaLegacyPuml https://raw.githubusercontent.com/eduardomozart/ArubaAirheads-PlantUML/main
!include ArubaLegacyPuml/puml/Service_Amigopod.puml
!include ArubaLegacyPuml/puml/Device_iphone.puml
!include ArubaLegacyPuml/puml/Laptop.puml

hide stereotype

skinparam {
    ArrowColor Black
    DefaultTextAlignment center
    BackgroundColor White
    shadowing false
    RoundCorner 10
    dpi 300
}

skinparam rectangle {
    BackgroundColor transparent
    BorderColor transparent
}

rectangle "<color:#2a5a72><$Service_Amigopod{scale=0.75}>" as CP
rectangle "<color:#2a5a72><$Device_iphone{scale=0.50}>" as Smartphone
rectangle "<color:#2a5a72><$Laptop{scale=0.75}>" as Laptop

CP -[hidden]- Laptop
CP <--> "\nEAP Exchange" Laptop : "<$Certificate{scale=0.75}>\nRADIUS"
CP <--> Smartphone : "<$Certificate{scale=0.75}>\nHTTPS"
@enduml
```
