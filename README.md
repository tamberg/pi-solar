# Pi Solar
Run a Pi on solar energy, initiated by [titipi.org](https://titipi.org/).

![pi-solar](https://github.com/user-attachments/assets/32765f14-62b0-44f6-b0d0-d919e0906cc4)

## Use the Pi
- Set up the solar panel
- Switch on the battery
- Use the Pi, e.g. as a
    - [Pi Etherpad Server](https://github.com/tamberg/pi-etherpad)
    - [Pi LoRaWAN Sensor](https://github.com/tamberg/pi-lora)
    - [Pi Timelapse Camera](https://github.com/tamberg/pi-cam)

# Make your own
## Get the hardware
- [Raspberry Pi 3 B+](https://www.pi-shop.ch/raspberry-pi-3-model-b) (CHF 34) or [Pi 4](https://www.pi-shop.ch/raspberry-pi-4-model-b-2gb) (CHF 49+)
- [Kingston SD card 16 GB](https://www.pi-shop.ch/kingston-microsdhc-karte-industrial-uhs-i-16-gb) (CHF 23; or similar)
- [Solar Panel 18V, 10W](https://www.pi-shop.ch/semi-flexible-polycrystalline-silicon-solar-panel-18v-10w-supports-5v-regulated-output) (CHF 20; or [this](https://www.bastelgarage.ch/18v-0-61a-monokristallines-solar-panel-10w), CHF 33)
- [Solar Power Manager](https://www.bastelgarage.ch/solar-power-manager-c-fur-6-24v-solar-panel) (CHF 24; or [this](https://www.pi-shop.ch/solar-power-manager), CHF 35)
- [Witty Pi Power Manager](https://www.pi-shop.ch/witty-pi-5-hat-realtime-clock-and-power-management-for-raspberry-pi) (CHF 45, plus a [battery](https://www.digitec.ch/en/s1/product/digitec-cr2032-lithium-8-pcs-cr2032-230-mah-batteries-36011518))
- 3 * [Li-Ion Battery 18650, 3200mA](https://www.bastelgarage.ch/li-ion-akku-3-7v-3200ma-ncr18650b-18650-mit-knopfpol?search=ncr18650b) (CHF 9)
- USB cable for Pi 3 B+ (Micro) or Pi 4 (USB-C)

## Get the tools
- Screw driver (might be included)
- USB Power Tester (optional)
- Soldering iron (optional)
- Wire cutter (optional)

## Open the solar power manager
![pi-solar-power-manager](https://github.com/user-attachments/assets/c0764fcd-574f-4199-b946-ac76b5bc6836)

## Add the Li-Ion batteries
Make sure the polarity (+/-) is as indicated.

![pi-solar-batteries](https://github.com/user-attachments/assets/126c9739-dacf-49b1-8bd4-8d0d2d56bbc2)

## Unsolder or cut clamps
![pi-solar-clamps](https://github.com/user-attachments/assets/a8c79344-5f25-45b9-b092-04e531234188)

![pi-solar-unsolder](https://github.com/user-attachments/assets/e631ffb1-9367-4a0c-955a-2f7fc5bf1b82)

## Screw wire terminals
The red clamp is plus (+), the black clamp is ground (-).

![pi-solar-screw-terminal](https://github.com/user-attachments/assets/df411616-36e3-4373-bf1e-a7104d271479)

## Connect all cables
![pi-solar-back](https://github.com/user-attachments/assets/cca3e249-260d-4acc-9c91-fa3e098ad096)

## Do the math
Use a power meter to measure voltage (V) and current (A), see how far one charge can get you.

![pi-solar-with-meter](https://github.com/user-attachments/assets/d5be96a8-c2db-40df-b5e8-180e2b145f8d)

## Manage power
Consider using a [Witty Pi 5](https://www.uugear.com/doc/WittyPi5_UserManual.pdf) power manager to switch the Pi on or off based on a schedule.

On your computer.

> Note: We assume your computer runs MacOS.

- Plug in the Witty Pi 5 hat via USB
- Wait for the _Witty Pi_ drive to mount
- Create a schedule with the [online editor](https://www.uugear.com/app/wittypi-scriptgen/
)
- Create a file _my.wpi_ on the drive
    ```bash
    $ sudo nano Witty\ Pi\ 5/schedule/my.wpi
    ```
    Paste the schedule, e.g.
    ```bash
	BEGIN 2025-01-01 11:00:00
	END   2035-12-31 23:59:59
	ON    H3 M0
	OFF   H21 M0
    ```
    Save with _CTRL-X-Y ENTER_
- Eject the _Witty Pi_ drive
- Unplug the hat from USB

On the Pi.

- Enable I2C (once) 
    ```bash
	$ sudo raspi-config # Interface Options > I2C > Yes
    ```
- Install the _wp5_ software (once)
    ```bash
	$ wget https://www.uugear.com/repo/WittyPi5/wp5_latest.deb
    $ sudo apt install ./wp5_latest.deb
    ```
- Add the hat to the Pi and insert a CR2032 battery
- Move USB power from the Pi to the Witty Pi 5 hat
- Press the big button on the hat to switch on the Pi
- Use the _wp5_ software to _write system time to RTC_
    ```bash
	$ wp5 # 1
    ```
- Use the _wp5_ software to _choose schedule script_
    ```bash
	$ wp5 # 6 > 1
    ```
- Observe the Pi switching on and off on schedule

## Limitations
- The solar panel might not allow 24 h usage
- Recharging the batteries might take time
- A Pi is not exactly a low power device

## License
This content by [@tamberg](https://twitter.com/tamberg) is licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).

## More
- https://www.flickr.com/photos/tamberg/albums/72177720325790438/ (Pi Solar Stand)
- https://www.raspberrypi.com/documentation/computers/getting-started.html
- https://www.waveshare.com/wiki/Solar_Power_Manager_(C)
