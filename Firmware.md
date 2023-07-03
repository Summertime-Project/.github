# Main MCU




# Modules

Network side of communication was shown here: [Communication.md](/Communication.md)

## Internal Data Structures and Data handling

..* Input buffer
..* Output buffer
..* Real state struct
..* Desired state struct (If closed loop only, else = Real)

## State struct

State struct storage is dependendent on Module.
It can store:
1. Primary Values accesed by Master:

- Velocity
- Angular velocity
- Position
- Angle
- Bolean Values (eg. Clamp state)

2. Secondary Values just like primary values (Porbably will not be used)

3. Internal Values:

- eg. servo angle
- eg. motor speed

## Communication Handling

### Incoming packets

Incoming packet (if posible should be filtered by lower level hardware communication protocol's handlers), should be transfered byte by byte to specialized buffer (From now known as inBuffer) of size **TODO** 256/512. 
CRC of packet should be checked first.
inBuffer should be checked if packet's module number matches MCU module nr. 

### Request Handling

If TLV is Request MCU should construct and send Actual data packet 