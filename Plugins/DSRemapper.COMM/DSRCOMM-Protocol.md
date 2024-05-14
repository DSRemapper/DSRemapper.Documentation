# DSRCOMM Protocol
## Description
This protocol was developed for communication with microcontrollers which supports serial comunication with a computer.

Originally created to be used over the RS-232 Protocol and with Arduino boards, **this protocol can be used on any asyncroneus byte-based communication** (like TCP/IP, for example).

_Note: This protocol is based on how HID (Human Interface Device) communication works. Therefore, it use reports and report IDs/Codes._

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
- **ACK:** In case of the DSRemapper sending data to the Device, it waits the ACK to prevent overwelming the device with data. In case of Arduino boards the Serial Port generates an interrupt, which can block the microcontroller and preventing it from read all the message from the buffer.

## Currently Defined Codes

### 0x00 - Info Report
Length: 32 bytes  
Description: Contains any information related to the connected device (in case of accelerometer or gyroscope, it's scale).

```c++
struct InfoReport{
  unsigned short AccelerometerScale;
  unsigned short GyroscopeScale;
}
```

### 0x01 - Default Input Status
Length: 64 bytes  
Description: Contains the data about the Device current status.

```c++
struct InputReport{
  
}
```

### 0x02 - Default Output Status
Length: 32 bytes + ACK (1 byte)  
Description: Contains the data to be send to the Device.

```c++
struct OutputReport{
  
}
```

### 0x03 - Output Status + Input Status as ACK
Lenght: 32 bytes + 64 bytes (As ACK)  
Description: Works as [Code 0x01](#0x01---default-input-status) and [Code 0x02](#0x02---default-output-status) combined. Sends status data to the Device and this send it's current status as an ACK.

Structures are the same as [Code 0x01](#0x01---default-input-status) and [Code 0x02](#0x02---default-output-status).