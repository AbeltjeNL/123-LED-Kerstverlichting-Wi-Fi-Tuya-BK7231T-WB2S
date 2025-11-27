# 123-LED-Kerstverlichting-Wi-Fi-Tuya-BK7231T-WB2S
123-LED-Kerstverlichting with Tuya BK7231T / WB2S

<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/27a38155-ffff-4453-8836-6d3acf0e755a" />

Hardware hacking the christmaslights adapter from [Smart adapter kerstverlichting 31V | Wifi](https://www.123led.nl/123led-Smart-adapter-kerstverlichting-31V-Wifi-i9442-t5928.html) into ESPHome.

- Verwijder het deksel van de adapter (hier zit de fysieke knop en de stekker aansluiting in) door de lijm verbinding te breken met een stuk gereedschap naar eigen keuze
- Verwijder de PCB met een platbek/telefoontang door deze naar buiten uit de behuizing te schuiven
- Soldeer passende draden op de volgende pinnen: 3V3, GND, TXT en RX
- Zorg dat je een extra draad (2e draad) soldeerd op de GND (deze kun je later verbinden met de CEN-pin
- Sluit vervolgens de gesoldeerde draden aan op jouw UART flasher volgens onderstaand diagram:
```
I:     --------+        +--------------------
I:          PC |        | BK7231             
I:     --------+        +--------------------
I:          RX | ------ | TX1 (GPIO11 / P11) 
I:          TX | ------ | RX1 (GPIO10 / P10) 
I:             |        |                    
I:         GND | ------ | GND                
I:     --------+        +--------------------
```

> [!IMPORTANT]
```The UART adapter's 3.3V power regulator is usually not enough. Instead, a regulated bench power supply, or a linear 1117-type regulator is recommended.```

- Sluit de externe 3V3 voedingsbron aan
- Verbind de UART adapter met een USB-poort op jouw systeem (zorg dat de juiste drivers geinstalleerd zijn) ;)
- Compile jouw ESPHome configuratie zodat je een .rbl bestand krijgt. Download dit bestand naar de "Downloads" map

> [!NOTE]
> Gebruik een van de flash tools van onderstaande link. Ik heb MacOS gebruikt. Met Windows is het helaas niet gelukt.
```https://docs.libretiny.eu/docs/flashing/tools/ltchiptool/#installation```

- Vanuit MacOS terminal voer je de volgende commando's uit: ```pip install ltchiptool``` & ```pip install wxPython```
- Navigeer naar de "Downloads" map. Als het goed is vind je hier jouw eerder gegenereerde ESPHome.rbl bestand
- Rechtermuisknop, onder aan in het venster op de map "Downloads" en selecteer "Open in Terminal"
- Zet de externe 3V3 voeding aan, de groene LED op de print begint te knipperen
- Voer het volgende commando uit in het terminal venster: ```ltchiptool flash write bestandsnaam.rbl```
- ltchiptool begint met het flashproces
- Raak nu met de extra GND draad de CEN pin kortstondig aan
- Je zult zien dat het flash proces nu begint
> [!CAUTION]
```Wees geduldig! Het flash proces kan even duren. Mocht de chip na het flashen niet booten, probeer het flash proces opnieuw.```
- Is het flashen voltooid? Mooi! Schakel de 3V3 voeding uit, koppel de UART adapter los en schakel de 3V3 voeding opnieuw in
- Ga naar het ESPHome dashboard en check via de draadloze logs of het zojuist geflashte apparaat online komt/is.

