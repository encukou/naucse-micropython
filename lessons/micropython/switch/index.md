## Další tlačítko

Teď si vezmi modul s tlačítkem a připoj ho k destičce:
`GND` vždycky na `G`, `VCC` vždycky na `3V` a
`OUT` na `D1`.

Tlačítko funguje tak, že `OUT` spojí buď s `VCC` (`3V`)
nebo `GND`, podle toho, jestli je tlačítko stisknuté.
(A navíc to taky teda svítí, ale to je teď vedlejší.)

Zkus si, jestli se zvládneš MicroPythonu zeptat, jestli je tlačítko zapnuté.
Mělo by to být podobné jako u příkladu s tlačítkem `FLASH`.


## Samostatné tlačítko

U samostatného tlačítka připoj `C` na `GND` a `NO` na `D1` (nebo jinou nožičku).

Vývod `NC` (angl. *not connected*, nezapojeno) nemusíš připojovat nikam,
je tam kvůli mechanické stabilitě.
