# Communication Protocol

## Mainframe - Main MCU communication

Modularity is built by designation of as many tasks and functions as close to physical effectors and sensors as posible. 
This dictates that Mainframe-MCU communication needs to transport as high level instrucions as possible but enough for robot to unambiguously determine desired state and for mainframe to determine actual state.

'''Frames and commands structure will be determined after internal discusion and consideration.'''

## Inter MCU communication

As one of project principles is modularity it's crucial to divide internal robot functions into different MCUs. To achive funcionality despite fragmentation there is need to implement some sort of inter MCU communication. 

### Physical Topology

Physical Topology of simple internal network needs to resemble physical divisions and take into consideration boundaries of interchangeable modules. We also can't assume homogeneity of low lewel protocols(eg. SPI) across all peripheral MCUs. Taking this requirements, we decided to use star network topology with one central MCU connects internal and external connections. This solution mitigate headaches of using different low level protocols. 

### Logical Topology

Logical Topology closely follows Physical Topology as it is also star, one master MCU connects master (Mainframe) to internal pheripherals and manages dataflow.
In future versions maybe we will implement some handshake protocol to make configuration easier.

# Conclusions

To conclude:
1. Communication needs to be bidirectional
2. To ease impementation there will be ladder of master hierarchy: Mainframe -> Main MCU -> Module MCU
3. Main MCU will be managing all trafic and all possible low level protocol transitions
4. All communication will be proceeded using ONE encapsulation and command set.