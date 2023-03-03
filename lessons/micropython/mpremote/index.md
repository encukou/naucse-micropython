## Práce se soubory

> [note]
> Budeme používat knihovnu `mpremote`, se kterou ještě nemáme tolik zkušeností.
> Kdyby něco nefungovalo, zkus kouknout na [starší návod](../ampy)
> který používá knihovnu `ampy`.
>
> Jestli se ti `mpremote` nepovedlo [zprovoznit](../install) a používáš
> `picocom`, Pytty nebo `screen`, přejdi na [starší návod](../ampy) hned.

Jak začneš psát trochu složitější programy,
mohlo by se stát, že tě konzole MicroPythonu začne trochu štvát.
Špatně se v ní opravují chyby a automatické odsazování funguje jen většinou.
Jak naštvání předejít?

Větší kousky kódu – a určitě takové,
ve kterých je nějaký cyklus, podmínka či funkce –
si piš v textovém editoru. MicroPythonu pak pošleš celý soubor.

Zkus si to. Do souboru `blikajici_led.py` dej následující kód:

```python
from machine import Pin
from time import sleep
pin_diody = Pin(14, Pin.OUT)
while True:
    print('blik!')
    pin_diody.value(0)
    sleep(1/2)
    pin_diody.value(1)
    sleep(1/2)
```

Předpokládám, že
Ve virtuálním prostředí bys měl{{a}} mít program `mpremote`.
[Návod na instalaci](../install)

Jestli máš otevřenou `mpremote` konzoli, zavři ji pomocí
<kbd>Ctrl</kbd>+<kbd>]</kbd>.
Potom `mpremote` pusť znovu, ale s podpříkazem `run` a názvem souboru:

```console
(venv)$ mpremote run blikajici_led.py
```

Program by měl blikat diodou.
Využívá k tomu funkci `time.sleep()`, která počká daný počet vteřin –
tedy `time.sleep(1/2)` zastaví program na půl sekundy.

Když zmáčkneš <kbd>Ctrl</kbd>+<kbd>C</kbd>, zavřeš `mpremote`.
Program poběží dál, ale neuvidíš výpisy (a chybové hlášky) které posílá.


## Nahrání souboru

Podobně je možné na destičku soubory i nahrávat, jen je potřeba místo
`run` použít `fs cp` se jménem souboru a dvojtečkou:

```console
(venv)$ mpremote fs cp blikajici_led.py :
```

Jak to funguje?  `fs cp <odkud> <kam>`.
Dvojtečka označuje soubor na destičce, na rozdíl od souborů na tvém
„velkém“ počítači.
Když zadáš dvojtečku samotnou, `cp` pro soubor na destičce použije stejné
jméno jako má soubor na „velkém“ disku.

To že je soubor nahraný si můžeš ověřit pomocí `fs ls`, který ukáže velikosti
a jména souborů na destičce:

```console
(venv)$ mpremote fs ls
ls :
         183 blikajici_led.py
         230 boot.py
```

## Automatické spouštění

Pokud navíc budeš chtít, aby se program na destičce automaticky spouštěl, musí
se soubor s programem na destičce jmenovat `main.py`. `mpremote` umí soubor při
kopírování i přejmenovat, když mu při kopírování zadáš za dvojtečkou
i druhé (nové) jméno:

```console
(venv)$ mpremote fs cp blikajici_led.py :main.py
```

Po úspěšném kopírování máš na destičce nahraný náš program ze souboru
`blikajici_led.py` do souboru `main.py`:

```console
(venv)$ mpremote fs ls
ls :
         183 blikajici_led.py
         183 main.py
         230 boot.py
```

Teď už bude tvůj program fungovat
i bez počítače, takže stačí destičku připojit např. k powerbance
a dioda se rozbliká.
Zkus to -- resetuj destičku jedním z těchto způsobů:

- odpojením a opětovným připojením USB kabelu
- tlačítkem RST na destičce
- příkazem `mpremote reset`

## Mazání a čtení

Soubor můžeš smazat pomocí příkazu `fs rm`:

```console
(venv)$ mpremote fs rm :main.py
```

Pak by měl být `main.py` smazaný:

```console
(venv)$ mpremote fs ls
ls :
         183 blikajici_led.py
         230 boot.py
```

A co že je to `boot.py`?
To je program který se spustí po zapojení destičky,
ještě před `main.py`.
Obsahuje nastavení.
Pomocí `fs cat` se můžeš podívat co dělá:

```console
(venv)$ mpremote fs cat boot.py
$ mpremote fs cat boot.py
# This file is executed on every boot (including wake-boot from deepsleep)
...
```
