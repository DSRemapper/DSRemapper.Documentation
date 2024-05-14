# DSRCOMM Protocol
## Description
This protocol was developed for communication with microcontrollers which supports serial comunication with a computer.

Originally created to be used over the RS-232 Protocol and with Arduino boards, **this protocol can be used on any asyncroneus byte-based communication** (like TCP/IP, for example).

_Note: This protocol is based on how HID (Human Interface Device) communication works. Therefore, it use reports and report IDs/Codes._

## Currently Defined Codes

### 0x00 - Info Report
Length: 32 bytes
Description: Contains any information related to the connected device (in case of accelerometer or gyroscope, it's scale)

<table>
  <thead>
    <tr>
      <th>Byte</th>
      <th>Bit 7</th>
      <th>Bit 6</th>
      <th>Bit 5</th>
      <th>Bit 4</th>
      <th>Bit 3</th>
      <th>Bit 2</th>
      <th>Bit 1</th>
      <th>Bit 0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td align=center colspan=8 rowspan=2>Acceleromeeter Scale</td>
    </tr>
    <tr>
      <td>1</td>
    </tr>
    <tr>
      <td>2</td>
      <td align=center colspan=8 rowspan=2>Gyroscope Scale</td>
    </tr>
    <tr>
      <td>3</td>
    </tr>
  </tbody>
</table>
