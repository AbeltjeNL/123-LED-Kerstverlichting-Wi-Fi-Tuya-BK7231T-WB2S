# 123-LED-Kerstverlichting-Wi-Fi-Tuya-BK7231T-WB2S
123-LED-Kerstverlichting with Tuya BK7231T / WB2S

<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/27a38155-ffff-4453-8836-6d3acf0e755a" />

Hardware hacking the christmaslights adapter from [Smart adapter kerstverlichting 31V | Wifi](https://www.123led.nl/123led-Smart-adapter-kerstverlichting-31V-Wifi-i9442-t5928.html) into ESPHome.

- Remove the adapter cover (this is where the physical button and plug connection are located) by breaking the adhesive bond with a tool of your choice
- Remove the PCB using flat nose/phone pliers by sliding it out of the housing
- Solder suitable wires (dupont) to the following pins: 3V3, GND, TX and RX
- Make sure to solder an extra wire (2nd wire) to GND (you can connect this to the CEN pin later)
- Next, connect the soldered wires to your UART flasher according to the diagram below:
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

- Connect the external 3V3 power source
- Connect the UART adapter to a USB port on your system (make sure the correct drivers are installed) ;)
- Compile your ESPHome configuration to create an .rbl file. Download this file to your Downloads folder.

> [!NOTE]
> Use one of the flash tools from the link below. I used macOS. Unfortunately, it didn't work with Windows.
```https://docs.libretiny.eu/docs/flashing/tools/ltchiptool/#installation```

- From MacOS terminal, run the following commands: ```pip install ltchiptool``` & ```pip install wxPython```
- Navigate to the "Downloads" folder. You should find your previously generated ESPHome.rbl file there
- Right-click on the "Downloads" folder at the bottom of the window and select "Open in Terminal"
- Turn on the external 3V3 power supply, the green LED on the PCB starts flashing
- Run the following command in the terminal window: ```ltchiptool flash write bestandsnaam.rbl```
- ltchiptool starts the flashing process
- Now briefly touch the CEN pin with the extra GND wire
- You will see the flash process start now
> [!CAUTION]
```Be patient! The flash process may take a while. If the chip doesn't boot after flashing, try the flash process again. If you see an error/retry, stop flashing and start again! ```
- Flashing complete? Great! Turn off the 3V3 power supply, disconnect the UART adapter, and turn the 3V3 power supply back on
- Go to the ESPHome dashboard and check via the wireless logs whether the device you just flashed comes/is online
- Node online? Great! Turn off the 3V3 power supply, desolder all wires, and check that all soldering is still correct
- Connect your (Christmas) lights and check whether they work as expected
- Yes? Great! Slide the PCB into its housing
- Take a hot glue gun (or other glue), squirt some glue into the edge of the lid and apply the lid to the adapter body
- Hold firmly (or fix)
- Enjoy! :)

> [!NOTE]
Write basic ESPHome yaml configuration and include LT-Hbeidge component @AbeltjeNL!
