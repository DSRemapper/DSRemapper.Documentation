# DSRemapper COMM Plugin

It's based on the Windows COMM Port. Intended for it's use with Arduino Boards to create game controllers in an easy way. It use the [DSRCOMM Protocol](./DSRCOMM-Protocol.md) for the communication.

_Note: for device development consult the DSRCOMM Protocol. In this wiki it's detailed what codes can be sended to the device._

## Considerations
- On [InfoReport](./DSRCOMM-Protocol.md#0x00---info-report), if `AccelerometerScale` or `GyroscopeScale` is 0, DSRemapper will not process Accelerometer and Gyroscopedata data. It will be available as Axes under Gyro and Accel Properties

## Device Detection
- This plugin use Windows WMI Querries to get the COMM Devices and their names.  
  _Originally it uses a standard C# function which checks the Windows Registry, but when unspected device disconnection happens the Windows Registry doesn't update until C# frees the COMM Port. That never happens because DSRemapper Framework frees the devices when it is no longer on the Windows Registry._

- The device name is obtained from the WMI Querry, for this reason, it will use the device name that Windows provides.

