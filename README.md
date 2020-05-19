# RFID-lock-unlock-a-computer
A university project that can lock and unlock any computer using a RFID Scanner and a tag.

## Index

1. [How it came to be](#how-it-came-to-be)

2. [Setting it up](#setting-it-up)
    - [Installation](#installation)
    - [Components](#components)
    - [Connections](#connections)
    - [Utilising the software](#utilising-the-software)
    - [Editing the code](#editing-the-code)
    - [Messing with the Firmware of ATmega16U2 for the UNO](#messing-with-the-firmware-of-atmega16u2-for-the-uno)

3. [Testing](#testing)

4. [Contributors](#contributors)

5. [License](#license)

## How it came to be
Dedicated to preventing password guessing, password theft, while providing an easier, and safer access to a computer.
This project came to be during the first semester at the university, and was also the first major project undertaken by me.

Finding a major issue in the fact that everyone utilised very simple passwords to unlock their computer, such as 'password', '123', 'admin123', most of which were easily crackable, either by guessing or by a bruteforce attack.

I hoped that people would up their security with harder to crack passwords which could be replaced on a weekly basis, hence, it was essential that complex passwords could be easily typed out without writing it down somewhere for people to come across.

## Setting it up

### Installation

The entire process requires the installation of multiple files like the [Arduino IDE](https://www.arduino.cc/en/Main/Software), and the [ATMEL Flip](http://ww1.microchip.com/downloads/en/DeviceDoc/JRE%20-%20Flip%20Installer%20-%203.4.7.112.exe).
The hex files, code, 
```
git clone https://github.com/dat-adi/RFID-lock-unlock-a-computer.git
```

The project essentially utilises the Arduino board combined with the RFID Scanner to act as the receiver for the signals transmitted by the RFID tags.

---

### Components

#### The hardware components you will require in order to set up and run this project are,

- Arduino Uno
- Jumper Wires
- Bread Board or PCB.
- RFID Scanner (RC522/MFRC522)
- RFID Tags

#### The software in order to configure the system would be,

- [Arduino IDE](https://www.arduino.cc/en/Main/Software), for the compiling and uploading of the code to the Arduino.
- [Atmel's FLIP 3.4.7](http://ww1.microchip.com/downloads/en/DeviceDoc/JRE%20-%20Flip%20Installer%20-%203.4.7.112.exe), this is used to implement the keystrokes into the Arduino which acts as a keyboard.

---

### Connections

The connections to be made for the working of this project are as follows,

| Pin   | Arduino UNO port| Colour |
| ----- |-----------------|--------|
| SDA   | D10             | Purple |
| MOSI  | D11             | Orange |
| MISO  | D12             | Green  |
| SCK   | D13             | Blue   |
| GND   | GND             | Black  |
| RST   | D9              | Blue   |
| 3.3V  | 3.3V            | Red    |

<p align="center">
    <img src="https://github.com/dat-adi/RFID-lock-unlock-a-computer/blob/master/assets/RFIDImage.png" alt="Connections" border="10"><br>
  connections
</p>

---

### Utilising the software

Add the MFRC522 library to your Arduino libraries, this ensures that you have all the required functions to manipulate the RFID Scanner into working the way it should.
[.zip](https://www.arduinolibraries.info/libraries/mfrc522) or, [GitHub hosted library](https://github.com/miguelbalboa/rfid)

After downloading/cloning either one of them into your computer, you'd want to extract it into your Arduino libraries, mostly located in the path given below, if you followed the default installation procedure.
```
C:\Program Files (x86)\Arduino\libraries
```

---

### Editing the code
Since the Arduino simply verifies whether or not a RFID tag can access the code, you need to change the code in order to let your tag access it.

This can be done using the tag's Unique Identifier code, also, known as *UID*.

#### UID identification
In order to change up the code, you first need to know what your tag's UID is.
<<<<<<< HEAD
For this, we use the program, *UID_identification*, you will find this [here](https://github.com/dat-adi/RFID-lock-unlock-a-computer/blob/master/arduino_codes/UID_identification/UID_identification.ino).
=======
For this, we use the program, *UID_identification*, you will find this [here](arduino_codes/UID_identification/UID_identification.ino).
>>>>>>> 47af3161a3090b9c788c7560d8f1212f9297cfd3

Running this code after uploading, we get the UID codes in the output screen, when the UID tags are brought close into proximity.
Store these somewhere in your system.

We will be needing these later.

#### Modifying the code to contain UID tags
Now, we need to modify the existing UID codes in the [RFID_use](arduino_codes/RFID_use/RFID_use.ino).
In [line 42](https://github.com/Naruita/RFID-lock-unlock-a-computer/blob/6ed9a8c351e9bd2d3f71e4363cc7bec0eaecb471/arduino_codes/RFID_use/RFID_use.ino#L42), we need to replace the UID codes as shown below,
<p align="center">
    <img src="https://github.com/Naruita/RFID-lock-unlock-a-computer/blob/master/assets/modify_code.PNG" alt="modify code" border="10">
    <br>
    UID modification
</p>

This will ensure that your RFID tag has access to the rest of the code, which registers keystrokes and prints them out as the password. Or, locks the computer by pressing a combination of Win key + L.

Now, you need to convert the password you want into the hex format of the password.
This can easily be done through the [hex file dictionary](/docs/USBKeyScan.pdf)

```C++
buf[0] = 0;
buf[2] = 0x04;          // letter A
Serial.write(buf, 8);   // Presses the key
releaseKey();           // Releases the key

delay(50);
```

Applied on the file RFID_use, [line 54](https://github.com/Naruita/RFID-lock-unlock-a-computer/blob/62748ac72d3d211d0a937e620e75145e14e52f4b/arduino_codes/RFID_use/RFID_use.ino#L54), just change the *0x04* which symbolizes 'A' to the letter you want through the hex file dictionary.

Continuing the same procedure for the rest of the letters, you should find yourself at completion with regards to making the hex password, in the Arduino code.

### Messing with the Firmware of ATmega16U2 for the UNO
This entire section is dedicated to changing the Arduino UNO into a keyboard, instructing it on which letters to insert into the system.

You will need to use the hex files present in this repository of mine, or find the hex files from the [source](https://github.com/coopermaa/USBKeyboard)

<p align="center">
    <img src="/assets/pin_connect.jpg"><br>
    Connecting pins
</p>

#### Steps to be followed in sequence from this point
1. Connecting the two pins as shown in the figure above.
2. Open ATMEL Flip, File -> Load Hex File. Use the [Arduino-Keyboard-0.3.hex](firmware/Arduino-Keyboard-0.3.hex) from [firmware files](firmware).
3. Run it.
4. Remove the USB and plug it in again.
5. Now, it acts as a keyboard, and you can proceed onto the testing phase.

#### Converting the board back into an Arduino Uno
The Arduino does no longer work as an Arduino in case you might have noticed.
This is because we have converted it into a keyboard.

We can convert it back into an Arduino Uno, simply by loading the [Arduino-usbserial-uno.hex](firmware/Arduino-usbserial-uno.hex) from [firmware files](firmware), and following the same procedure, as the ones above.

## Testing
> The board has to be in the keyboard state for this to work, or else, it won't pass any keystrokes to the computer.

Now, proceeding onwards, we can upload the code to the Arduino and test it.<br>
Once the connected computer is in either a lock or unlocked state, bring the RFID tag to a proximity of 5 cm, in order to test it's usage.

It should lock/unlock the computer depending on which state it was in previously.

---

## Contributors
Being a project made in university, this project was contributed to by [@1StranGe](https://github.com/1StranGe) as a team member.

## License
This project is now hosted under the MIT License.
