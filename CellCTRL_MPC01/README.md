# CellCTRL Electric

Das MPC01 Board wurde für den Manipulator der KTLA ausgelegt.

Aktoren Anschluss:
4x (TMC2009) Stepper Motor
2x Servo Motor

Sensorik:
3x Endschalter (XYZ)


Bus Systeme:
I2C (Für Test Controller im Test Betrieb) (Ausgeführt über SDA und SCL) Nur bei UNO R3 vorhanden
RS485 Kommunikation einzelner Module zu einer Fertigungskette


## 🛠 Skills
Löten, Basic Bauteilkunde, 


## MPC01

#### Usage:
Der MPC01 Controller ist für die Steuerung von 3 Stepper Motoren (TMC2209 Treiber) mit jeweils einem Endschlater designt. Es können über I2C noch weitere Module mitangesteuert werden, wie den MPC-Servo und MPC-Status. Über RS485 sollen mit den anderen Module der Produktionsstraße kommuniziert werden können. (Error Übergabe, Befehle, etc.) Mit der Anbindung von PDNUart, ist es möglich den Motor nach dem Einschalten zu konfigurieren.


![MPC01_Top](https://github.com/Kappi084/CellCTRL/blob/main/CellCTRL_MPC01/MPC01/MPC01_Top.png)
![MPC01_Bottom](https://github.com/Kappi084/CellCTRL/blob/main/CellCTRL_MPC01/MPC01/MPC01_Back.png)

#### Features:
3x Steppermotor
3x Endschalter 
1x Notaussignal (Enable_Stepper) (NC)
1x I2C
1x RS485

| Connector | Arduino Pin     | Description                |
| :-------- | :------- | :------------------------- |
| `Endstop Z` | `A0` | NC_Endstop |
| `Endstop Y` | `A1` | NC_Endstop |
| `Endstop X` | `A2` | NC_Endstop |
| `RS485_DE/RE` | `A3` | RS485 |
| `SDA/SCL` | `A4` | I2C |
| `SDA/SCL` | `A5` | I2C |
| `DIR 3` | `D2` | Motor 3 |
| `STEP 3` | `D3` | Motor 3 |
| `DIR 2` | `D4` | Motor 2 |
| `STEP 2` | `D5` | Motor 2 |
| `DIR 1` | `D6` | Motor 1 |
| `STEP 1` | `D7` | Motor 1 |
| `TX` | `D8` | PDNUart StepperMotor |
| `RX` | `D9` | PDNUart StepperMotor |
| `RS485 TX` | `D10` | RS485 |
| `RS485 RX` | `D11` | RS485 |
| `PGOOD` | `D12` | Power OK 5V |
| `Enable` | `D13` | Enable Stepper Motor (Notaus) |


### ⚠️ Notes
Um PDNUART verwenden zu können, müssen mit Jumper bei MS1 und MS2 noch die richtigen Adressen eingestellt werden.

## MPC_Servo

#### Usage:
Der MPC_Servo Controller wird über I2C angesteuert, und kann entweder zwei Servos oder einen Servo und einem Endschalter betrieben werden.


#### Features:
1x Servo
1x Servo/Endschalter

![MPC_Servo_Top](https://github.com/Kappi084/CellCTRL/blob/main/CellCTRL_MPC01/MPC_Servo/MPC_Servo.png)

#### Schnittstellenbescreibung:



## MPC_Status

#### Usage:
Der MPC_Status Controller wird ebenfalls mit I2C gesteuert, und wirkt somit wie der Servo ein "Modul". Mit dem ist es möglich, den jeweiligen Status der Anlage anzuzeigen mithilfe von LEDs.

#### Features:
1x LED Statuslicht

| Color | Status     | Description                |
| :-------- | :------- | :------------------------- |
| Blau leuchtend | Boot | Bei hochfahren der Anlage |
| Blau blinkend | Homing | Beim Homen und Initialisieren der Anlage |
| Grün leuchtend | Ready | Die Anlage steht, aber ist Bereit für Befehle |
| Gelb leuchtend | Auto | Ist im Automatikbetrieb, und steht |
| Gelb blinkend | Manual | Ist im Manuelen Betrieb, und steht |
| Rot leuchtend | Moving | Die Anlage bewegt eine Achse etc. |
| Rot blinkend | EStop | Der Not Aus wurde betätigt, muss Quittiert werden! |
| Rot drehend | Error | Es liegt ein Fehler bei der Anlage an! (Quittierung notwendig) |

![MPC_Status_Top](https://github.com/Kappi084/CellCTRL/blob/main/CellCTRL_MPC01/MPC-Status/MPC-Status_Top.png)
![MPC_Status_Bottom](https://github.com/Kappi084/CellCTRL/blob/main/CellCTRL_MPC01/MPC-Status/MPC-Status_Back.png)

#### ⚙️ Configuration I2C_Status

- **I²C Address:** `0x3C`
- **Bus Speed:** Up to 400kHz (Fast Mode)
- **Addressing Mode:** 7-bit

#### 📋 Register Map I2C_Status

| Address | Name        | R/W | Description              |
|--------|------------|-----|--------------------------|
| 0x00   | STATUS     | R   | Device status register   |
| 0x01   | CONTROL    | R/W | Control settings         |
| 0x02   | TEMP_MSB   | R   | Temperature (MSB)        |
| 0x03   | TEMP_LSB   | R   | Temperature (LSB)        |

#### 🔄 Example
```cpp
// example code
