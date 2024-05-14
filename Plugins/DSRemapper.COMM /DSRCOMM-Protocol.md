# DSRCOMM Protocol
## Description
This protocol was developed for communication with microcontrollers which supports serial comunication with a computer.

Originally created to be used over the RS-232 Protocol and with Arduino boards, **this protocol can be used on any asyncroneus byte-based communication** (like TCP/IP, for example).

_Note: This protocol is based on how HID (Human Interface Device) communication works. Therefore, it use reports and report IDs/Codes._

## Communication structure

In any case, DSRemapper will iniciate or solicitate the communication sending a code. But there is 2 types of communication, DSRemapper sending data to the Device and the Device sending data to DSRemapper

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
- **ACK:** In case of the DSRemapper sending data to the Device, it waits the ACK to prevent overwelming the device with data. In case of Arduino boards the Serial Port generates an interrupt, which can block the microcontroller and preventing it from read all the message from the buffer.

## Currently Defined Codes

### 0x00 - Info Report
Length: 32 bytes  
Description: Contains any information related to the connected device (in case of accelerometer or gyroscope, it's scale)

```c++
struct InfoReport{
  short AccelerometerScale;
  short GyroscopeScale;
}
```
