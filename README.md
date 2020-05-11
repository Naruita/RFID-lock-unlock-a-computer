# RFID-lock-unlock-a-computer
A university project that can lock and unlock any computer using a RFID Scanner and a tag.

## Index

1. [How it came to be](#how-it-came-to-be)

2. [Setting it up](#setting-it-up)
    - [Installation](#installation)
    - [Components](#components)
    - [Connections](#connections)
    - [Utilising the software](#utilising-the-software)
    - [Editing the code](editing-the-code)

3. [Contributors](#contributors)

4. [License](#license)

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
git clone https://github.com/Naruita/RFID-lock-unlock-a-computer.git
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
    <img src="https://github.com/Naruita/RFID-lock-unlock-a-computer/blob/master/assets/RFIDImage.png" alt="Connections" border="10"><br>
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
For this, we use the program, *UID_identification*, you will find this [here](https://github.com/Naruita/RFID-lock-unlock-a-computer/blob/master/arduino_codes/UID_identification/UID_identification.ino).

Running this code after uploading, we get the UID codes in the output screen, when the UID tags are brought close into proximity.
Store these somewhere in your system.

We will be needing these later.

#### Modifying the code to contain UID tags

---

## Contributors
Being a project made in university, this project was contributed to by [@1StranGe](https://github.com/1StranGe) as a team member.

## License
This project is now hosted under the MIT License.
