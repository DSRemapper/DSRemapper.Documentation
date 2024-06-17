# DSRemapper COMM Plugin

It's based on the Windows COMM Port. Intended for it's use with Arduino Boards to create game controllers in an easy way. It use the [DSRCOMM Protocol](./DSRCOMM-Protocol.md) for the communication.

## Device Development
- For device development consult the [DSRCOMM Protocol](./DSRCOMM-Protocol.md). In this wiki it's detailed what codes can be sended to the device and how it needs to answer.

- This plugin will ONLY send codes requiered to achieve the functionality, some codes defined on the [DSRCOMM Protocol](./DSRCOMM-Protocol.md) may not be used by this plugin.

## Considerations
- On [InfoReport](./DSRCOMM-Protocol.md#0x00---info-report), if `AccelerometerScale` or `GyroscopeScale` is 0, DSRemapper will not process Accelerometer and Gyroscopedata data. It will be available as Axes under Gyro and Accel Properties

## Device Detection
- This plugin use Windows WMI Querries to get the COMM Devices and their names.  
  _Originally it uses a standard C# function which checks the Windows Registry. But when unexpected device disconnection happens, the Windows Registry doesn't update until C# closes and frees the COMM Port. That never happens because DSRemapper Framework frees the devices when it is no longer on the Windows Registry._

- The device name is obtained from the WMI Querry, for this reason, it will use the device name that Windows provides.

## [DSRCOMM Protocol](./DSRCOMM-Protocol.md) Used Codes
This are the codes used by this plugin:
- [`0x00` code](./DSRCOMM-Protocol.md#0x00---info-report-1) [^1]
- [`0x01` code](./DSRCOMM-Protocol.md#0x01---default-input-status-1) [^1]
- [`0x02` code](./DSRCOMM-Protocol.md#0x02---default-output-status-1) [^1]
- [`0x03` code](./DSRCOMM-Protocol.md#0x03---output-status--input-status-as-ack) [^2]

[^1]: This operation is required by this plugin
[^2]: This operation will be requested by this plugin if [ReportACK](#0x00---info-report-1) bit is 1
