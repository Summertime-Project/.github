# Main MCU




# Modules

Network side of communication was shown here: [Communication.md](/Communication.md)

## System Architecture

For all modules' software to be expandable we need specific approach to system design.
Funcionalities that all modules are in need of:

- Reading and writing dataframes to Bus
- Steering peripherals
- Reading peripherals
- _Error throwing and handling_

For foreseeable future all software will be run in a totally deterministic blocking superloop, where the following tasks will be executed:

- Read dataframe from Bus, validate and decode, update desired state struct

- Read from peripherals, update internal state, calculate and update accessible (by master) state using internal state

- Construct dataframe, write it to bus

- Calculate internal state using state structs, update peripherals


_Errors should be thrown on bus when master requests any info from module_.

All modules should have switchable debug logging through USB.

## Internal Data Structures and Data handling

- Input buffer
- Output buffer
- Real state struct
- Desired state struct (If closed loop only, else = Real)

## State struct

State struct storage is dependendent on Module.
It can store:
1. Values accesed by Master:

- Velocity
- Angular velocity
- Position
- Angle
- Boolean Values (eg. Clamp state)

3. Internal Values:

- servo angle
- motor speed
- etc.

## Communication Handling

### Incoming packets

Incoming packet (if posible should be filtered by lower level hardware communication protocol's handlers), should be transfered byte by byte to specialized buffer (inBuffer) of size **TODO** 256/512. 
CRC of packet should be checked first. Then, the recipient module number included in the packet should be compared to the actual module's nubmer.

### Request Handling

When TLV is Request, MCU should construct and send a data packet containing an actual state variable.
