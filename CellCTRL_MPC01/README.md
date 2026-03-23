#CellCTRL Electric

Das MPC01 Board wurde für den Manipulator der KTLA ausgelegt.

Aktoren Anschluss:
4x (TMC2009) Stepper Motor
2x Servo Motor

Sensorik:
3x Endschalter (XYZ)


Bus Systeme:
I2C (Für Test Controller im Test Betrieb) (Ausgeführt über SDA und SCL) Nur bei UNO R3 vorhanden
RS485 Kommunikation einzelner Module zu einer Fertigungskette


![Schaltplan](CellCTRL_MPC01/MPC01/Schaltplan_MPC01.pdf)


## 🛠 Skills
Löten, Basic Bauteilkunde, 


##MPC01

####Usage:
Der MPC01 Controller ist für die Steuerung von 3 Stepper Motoren (TMC2209 Treiber) mit jeweils einem Endschlater designt. Es können über I2C noch weitere Module mitangesteuert werden, wie den MPC-Servo und MPC-Status. Über RS485 sollen mit den anderen Module der Produktionsstraße kommuniziert werden können. (Error Übergabe, Befehle, etc.) Mit der Anbindung von PDNUart, ist es möglich den Motor nach dem Einschalten zu konfigurieren.


https://github.com/Kappi084/CellCTRL/blob/main/CellCTRL_MPC01/MPC01/MPC01_Top.png


####Features:
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



##MPC_Servo


##MPC_Status
