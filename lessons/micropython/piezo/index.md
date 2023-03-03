## Tóny a melodie

Vezmi si další součástku – piezobudič, neboli „bzučítko”.

Tahle malá věc obsahuje speciální materiál, který se,
když ho připojíš ke zdroji napětí, trošku roztáhne.
Roztažením zatlačí na okolní vzduch a vytvoří tlakovou
vlnu, která může doputovat až k tvým uším.

Zkus si to – když jednu nožičku bzučítka připojíš na `GND`
(tentokrát je jedno kterou) a druhou budeš přepojovat mezi `3V`
a `GND`, uslyšíš vždy tiché lupnutí.

Co se stane, když budeš napětí připojovat a odpojovat, řekněme, 32× za vteřinu?
Nebo 65×?

{% filter solution %}
Ozve se tón!
{% endfilter %}

Zkus si vybrat z následujících frekvencí.·
Hz – [Hertz](https://en.wikipedia.org/wiki/Hertz) – je jednotka frekvence;
„49 Hz“ znamená „49× za sekundu“, neboli `PWM.freq(49)`.
MicroPython umí jen celočíselné frekvence, takže zaokrouhluj.

| Nota | Frekvence |
|:-----|----------:|
| C1   | 32,70 Hz  |
| D    | 36,71 Hz  |
| E    | 41,20 Hz  |
| F    | 43,65 Hz  |
| G    | 49,00 Hz  |
| A    | 55,00 Hz  |
| H    | 61,74 Hz  |
| C2   | 65,41 Hz  |

Teď si můžeš naprogramovat písničku!
Potřebuješ-li víc not, pusť si [program](static/noty.py),
který vypočítá další frekvence.
