# jump
ROS interface to communicate with ST FOC board

## The MCP(Motor Control Protocol) in brief:
UART Baud 9600 by default
Code(1 byte)+Size(1 byte)+Payload(<Size> bytes)+CRC(1 byte)
```C
uint16_t checksum=Code xor Size xor PayloadByte1 xor ... xor PayloadByteN;
uint8_t CRC=(checksum&0xFF)+(checksum>>8); //High 8 bits plus low 8 bits
//this should not be called CRC at all as it only checks for errors but cannot recover the error bit
```
### Code:
**0x06** GetBoardInfo \
**0x22** Selects Motor \
**0x03** SendControlCmd 

### Example:
**06 00 06** Get Board Info \
**03 01 01 05** Start Motor \
**03 01 02 06** Stop Motor 
