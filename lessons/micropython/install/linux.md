# Instalace pro Linux

Na správně nastaveném počítači stačí zadat:

```console
$ picocom -b 115200 --flow n /dev/ttyUSB0
```

Pokud příkaz neskončí s chybou, stiskni tlačítko `RST` na modulu.
Měly by se nakonec objevit tři zobáčky, `>>>`.

Většina počítačů ale na komunikaci s malými zařízeními nastavená není.
Skončí-li příkaz `picocom` s chybou,
oprav ji podle následujícího návodu a zkus to znova.
(Možná bude potřeba vyřešit víc než jednu chybu.)

* Nemáš-li příkaz `picocom` nainstalovaný,
  je potřeba ho nainstalovat (např.
  `sudo dnf install picocom` nebo
  `sudo apt-get install picocom`).
* Pokud `picocom` skončil s chybou
  `No such file or directory`, pravděpodobně
  je potřeba k zařízení přistupovat přes jiný soubor.
  Použij příkaz `dmesg | tail`, který vypíše něco jako:

  <pre>
  $ dmesg | tail
  [703169.886296] ch341 1-1.1:1.0: device disconnected
  [703176.972781] usb 1-1.1: new full-speed USB device number 45 using ehci-pci
  [703177.059448] usb 1-1.1: New USB device found, idVendor=1a86, idProduct=7523
  [703177.059454] usb 1-1.1: New USB device strings: Mfr=0, Product=2, SerialNumber=0
  [703177.059457] usb 1-1.1: Product: USB2.0-Serial
  [703177.060474] ch341 1-1.1:1.0: ch341-uart converter detected
  [703177.062781] usb 1-1.1: ch341-uart converter now attached to <strong>ttyUSB0</strong>
  </pre>

  Jestli tyhle řádky nevidíš, zkus destičku odpojit, znovu zapojit a spustit
  `dmesg | tail` znovu.

  Máš-li místo `ttyUSB0` něco jiného, v příkazu `picocom` to použij místo
  `ttyUSB0`.

* Pokud `picocom` skončil s chybou `Permission denied`, potřebuješ získat
  přístup k souboru zařízení.
  To znamená přidat se do příslušné skupiny:

  ```console
  $ sudo usermod -a -G dialout $(whoami)
  ```

  Poté je potřeba se znovu přihlásit, třeba příkazem:

  ```console
  $ su - $(whoami)
  ```

  Pro ověření spusť příkaz `groups`; v jeho výstupu by mělo být `dialout`.
  Například:

  ```console
  $ groups
  kristyna lp wheel dialout mock
  ```

