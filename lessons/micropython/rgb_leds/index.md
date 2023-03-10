
## Barevná světýlka

Je čas na novou hračku!
Tentokrát to bude LED pásek.

Na pásku máš 8 malých čtverečků.
Každý z nich obsahuje docela hodně elektroniky:
tři barevné LED (červenou, zelenou a modrou)
a čip, který je umí ovládat pomocí informací,
které dostane přes jediný drátek z modulu.

Takové pásky se prodávají po metrech a dají se
nastříhat – mezi jednotlivými světýlky si všimni čárky,
která naznačuje, kde máš střihnout.
Energie z USB stačí zhruba na osm světýlek, proto jsi jich dostal{{a}} tolik.

Tenhle LED pásek je stavěný na pět voltů. Naštěstí ale potřebuje 5 V jen
na <em>napájení</em>; řídící signál s informacemi o barvičkách může mít 3,3 V.

Pojďme pásek zapojit:

* `GND` pásku (bílý drátek) připoj na `G`
* `DI` (*data in* – zelený drátek) připoj na `D4`
* `+5V` (červený drátek) připoj na `Vin`.

> [warning]
> Nožička `Vin` poskytuje 5 voltů.
> Pozor na ni: připojuj na ni jen zařízení které umí pracovat s pěti volty!
>
> Například modrá dioda, která je „dělaná“ na 3V, bude s pěti volty svítit
> velice jasně, ale jen chvilku a pak zhasne navždy.
> Jiná zařízení múžou být podobně choulostivá.
>
> `Vin` znamená *vstupní napětí* (angl. *input voltage*).
> U USB je to 5V, ale až budeš destičku „krmit“ ze čtyř AAA baterií,
> na `Vin` bude dokonce 6 voltů.

Máš-li zapojeno, můžeš začít programovat.
„Jazyk” kterým „mluví” tenhle LED pásek je trošku
složitější než signál PWM, ale MicroPython obsahuje
speciální knihovnu, která s páskem komunikovat umí.
Vypadá to nějak takhle:


<pre>
from machine import Pin
from neopixel import NeoPixel

POCET_LED = 8
pin = Pin(2, Pin.OUT)
np = NeoPixel(pin, POCET_LED)
np<span class="highlight-nocolor">[0]</span> = (<span class="highlight-red">255</span>, <span class="highlight-green">255</span>, <span class="highlight-blue">255</span>)
np.write()
</pre>


Co znamenají ta čísla (`0` a `255`), na to už jistě přijdeš {{gnd('sám', 'sama')}}.
Jen při experimentování nezapomeň zavolat
`np.write()`, tím se informace pošlou do LED pásku.

Zvládneš naprogramovat semafor?
