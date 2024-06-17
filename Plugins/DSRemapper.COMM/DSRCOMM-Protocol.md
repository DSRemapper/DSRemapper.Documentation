# DSRCOMM Protocol
## Description
This protocol was developed for communication with microcontrollers which supports serial comunication with a computer.

Originally created to be used over the RS-232 Protocol and with Arduino boards, **this protocol can be used on any asyncroneus byte-based communication** (like TCP/IP, for example).

_Note: This protocol is based on how HID (Human Interface Device) and DirectInput communication works. Therefore, it use reports and report IDs/Codes._

## Communication structure

In any case, DSRemapper will iniciate or solicitate the communication sending a code. But there is 2 types of communication, DSRemapper sending data to the Device and the Device sending data to DSRemapper.

### DSRemapper to Device Data
|        | Code       | Structure   | ACK    |
|--------|------------|-------------|--------|
| Length | 1 Byte     | 32-64 Bytes | 1 Byte |
| Sender | DSRemapper | DSRemapper  | Device |

### Device to DSRemapper Data
|        | Code       | Structure   |
|--------|------------|-------------|
| Length | 1 Byte     | 32-64 Bytes |
| Sender | DSRemapper | Device      |

### Parts Description
- **Code:** Equivalent to the HID report ID. Represented by 1 byte it tells to the device what operation needs to be performed.

- **Structure:** The data structure that is sended can be 32 or 64 bytes size (this size are defined to provide a default standard).

- **ACK:** In case of the DSRemapper sending data to the Device, it waits the ACK (or a defined timeout, if the ACK is never received) to prevent overwhelming the device with request ot data. In case of Arduino boards the Serial Port generate interrupts, which can block the microcontroller and prevent it's normal code execution.

### ACK Byte
The ACK byte needs to be diferent from -1 or 255 (`0xFF` on Hex). The default behaviour of this byte is to unlock DSRemapper from a wait state and complete the comunication with the device. If this byte is not sended DSRemapper will wait for a timeout.

_Note: If the behaviour of this byte is changed, the values will be documented here_

## Currently Defined Codes

### 0x00 - Info Report [^1]
Length: 32 bytes  
Description: Contains any information related to the connected device (in case of accelerometer or gyroscope, it's scale).

```c++
struct InfoReport{
  byte ReportIdCount; // If this value is more than one, DSRemapper will spect multiple Input Reports per request
  unsigned short AccelerometerScale;
  unsigned short GyroscopeScale;
  byte ReportACK : 1; // Report as ACK. If set, then DSRemapper will use 0x03 Code for data retrive
  byte CRC16 : 1; // if set, DSRemapper will expect a CRC16 on the last bytes of the InputReport and the OutputReport. Otherwise, this bytes can be used for data transfer
  byte CustomName : 1; // if set, DSRemapper will request a custom name with 0x10 code
  byte reserved : 5;
  byte reserved[27];
}
```

### 0x01 - Default Input Status [^1]
Length: 64 bytes  
Description: Contains the data about the Device current status.

```c++
struct InputReport{
  byte Id; // Aditional id to support multiple InputReport for one device
  short Axes[6];
  short Pov0;
  byte Buttons[4];
  short Accelerometer[3]; // X, Y and Z axes
  short Gyroscope[3]; // X, Y and Z axes
  byte Battery;
  short Sliders[6];
  short Pov1; // Aditional Pov
  byte ButtonsExt[4]; // Aditional Buttons
  short AxesExt[6]; // Aditional Axes
  byte CRC16[2];
}
```

### 0x02 - Default Output Status [^1]
Length: 32 bytes + ACK (1 byte)  
Description: Contains the data to be send to the Device.

```c++
struct OutputReport{
  byte Id; // Aditional id to support multiple InputReport for one device
  short Axes[6];
  byte Buttons[4];
  byte reserved[13];
  byte CRC16[2];
}
```

### 0x03 - Output Status + Input Status as ACK
Lenght: 32 bytes + 64 bytes (As ACK)  
Description: Works as [Code 0x01](#0x01---default-input-status-1) and [Code 0x02](#0x02---default-output-status-1) combined. Sends status data to the Device and this send it's current status as an ACK.

Structures are the same as [Code 0x01](#0x01---default-input-status-1) and [Code 0x02](#0x02---default-output-status-1).

### 0x10 - Custom Name
Length: 0 - 50 bytes + '\0' character
Description: Sends a custom name from the device to DSRemapper, the response is a null terminated string.

[^1]: This operation needs to be implemented on the COMM device for this protocol to work
