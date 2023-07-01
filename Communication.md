# Communication Protocol

## Inter MCU communication

As one of project principles is modularity it's crucial to divide internal robot functions into different MCUs. To achive funcionality despite fragmentation there is need to implement some sort of inter MCU communication. 

### Physical Topology

Physical Topology of simple internal network needs to resemble physical divisions and take into consideration boundaries of interchangeable modules. We also can't assume homogeneity of low lewel protocols(eg. SPI) across all peripheral MCUs. Taking this requirements, we decided to use star network topology with one central MCU connects internal and external connections. This solution mitigate headaches of using different low level protocols. Interconnectors between modules will be easily dettached and reattached.  

### Logical Topology

Logical Topology closely follows Physical Topology as it is also star, one master MCU connects master (Mainframe) to internal pheripherals and manages dataflow.
In future versions maybe we will implement some handshake protocol to make configuration easier.

## Mainframe - Main MCU communication

Modularity is built by designation of as many tasks and functions as close to physical effectors and sensors as posible. 
This dictates that Mainframe-MCU communication needs to transport as high level instrucions as possible but enough for robot to unambiguously determine desired state and for mainframe to determine actual state.

To ensure fast and robust communication Main MCU will buffer all incoming data and if there won't be update, retransfer it as required.

# Structure 
## Big encapsulation
Big encapluation task is to provide direct and errorless Body transfer between nodes.

|CONF - 1| LEN - 1 | BODY - LEN | CRC - 1|
|---|---|---|---|
    
### CONF

|bit |Short |Desc |
|--- |---- |---- |
|0| RFU||
|1| RFU||
|2| RFU||
|3| RFU||
|4| RFU||
|5| MNR0||
|6| MNR1||
|7| MNR2||

|MNR| Module|
|---|---|
|0| Main (sholud not used)|
|1| Chassis|
|2| Arm|
|3| Cam Turret|
|4| Prox|

### LEN
 
 Uint8 encoding BODY lenght, can be 0.

### BODY

TLV encapsulated Data

### CRC
One byte CRC wil be derrived from LEN and BODY

## DER-TLV Encapsulation

[Der-TLV](https://www.oss.com/asn1/resources/asn1-made-simple/asn1-quick-reference/basic-encoding-rules.html)

### Private Tags

#### Primitive
|Num |Name |Desc |Simillar Type |
|--- |---- |---- |---- |
|0| REQUEST| requests data from slave, in Value should be requested tag| UINT16|
|1| RFU|||
|2| CO1| Primary Open/Closed| BOOL(DER???     FF=True, 00=False, else error?)|

#### Constructed
|Num |Name |Desc | Containing|
|--- |---- |---- | ----------|
|0| ALL| All available data transfered inside this tag !!!Dificult!!!| device specific|
|1| V1| Velocity 1|         3xINT32/FLOAT|
|2| W1| Angular velocity 1| 3xINT32/FLOAT|
|3| P1| Position 1|         3xINT32/FLOAT|
|4| A1| Angle 1|            3xINT32/FLOAT|

## Examples

|C0|01|V1||

## Data Stored and Processed
**Accesible by master**, _Planned_. All shown below informations inside systems are desired an actual if open close loop controll is used.  

#### by Arm MCU

* Arm servo position
* Clamp servo position
* **Arm cartesian position**
* _Arm cartesian orientation_
* **Clamp state**

#### by Chasis MCU

* Motors' velocity (open loop)
* _Motors' position_
* _Chassis cartesian position_
* _Chassis cartesian angle_
* **Chassis relative velocity**
* **Chassis relative angular velocity**

#### by Obstacles Sensor MCU

* **Obstacles cartesian position**
* Sensors proximity signals

#### by Main MCU

* **Arm cartesian position**
* **Clamp state**
* **Chassis relative velocity**
* **Chassis relative angular velocity**
* **Obstacles cartesian position**

# TODO

To conclude:
1. Communication needs to be bidirectional
2. To ease impementation there will be ladder of master hierarchy: Mainframe -> Main MCU -> Module MCU
3. Main MCU will be managing all trafic and all possible low level protocol transitions
4. All communication will be proceeded using ONE encapsulation and command set.
5. Each element of network will store and process data necessary to properly execute dedicated functions. 