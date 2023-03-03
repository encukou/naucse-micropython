## Flashování

Na našich destičkách je MicroPython už nahraný, ale kdyby sis koupil{{a}}
vlastní NodeMCU nebo chtěl{{a}} firmware aktualizovat, budeš ho potřebovat umět
nahrát.

K tomu je potřeba nástroj `esptool`, který se dá nainstalovat pomocí:

```console
(env)$ python -m pip install esptool
```

Po instalaci esptool si stáhni nejnovější stabilní firmware pro ESP8266
z [https://micropython.org/download/esp8266/](https://micropython.org/download/esp8266/).
a zadej:

```console
(env)$ esptool.py --port /dev/ttyUSB0 --baud 230400 write_flash 0 esp8266-20161110-v1.8.6.bin
```

Hodnotu pro `--port` opět doplň podle svého systému – např. `/dev/tty.wchusbserial1420` na Macu, `COM3` na Windows.
Jméno souboru (poslední argument) použij podle toho co jsi stáhl{{a}}.

> [note]
> Destiček s čipem ESP8266 se vyrábí celá řada různých typů a některé mohou
> potřebovat odlišné nastavení při flashování.
> Popis všech možností nastavení je k nalezení v [dokumentaci k esptool](https://github.com/espressif/esptool#usage).
>
> Občas je potřeba nastavit [volbu `--flash_mode`](https://docs.espressif.com/projects/esptool/en/latest/esp8266/advanced-topics/spi-flash-modes.html)
> na konkrétní hodnotu (`qio`, `qout`, `dio`, `dout`).
> Kterou přesně je asi nejjednodušší zjistit experimentálně.
>
> Některé problémy vyřeší nižší rychlost: `--baud 112500`.
>
> Některé problémy vyřeší detekce velikosti Flash paměti: `--flash_size detect`.

Je-li na desce nahraný firmware, tento příkaz by měl fungovat. U jiného
firmware, případně u poškozeného MicroPythonu, je potřeba při resetu
(nebo zapojování destičky do USB) držet tlačítko FLASH.
