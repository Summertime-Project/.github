# Communication Protocol

## Inter MCU communication

As one of the project's principles is modularity it's crucial to divide internal robot functions into different MCUs. To achive funcionality despite fragmentation there is a need to implement some sort of internal MCU communication. 

### Physical Topology

Physical Topology of simple internal network needs to resemble physical divisions and take into consideration boundaries of interchangeable modules. We also can't assume homogeneity of low lewel protocols (eg. SPI) across all peripheral MCUs. Having considered those requirements, we decided to use star network topology with one central MCU connecting internal and external connections. This solution mitigates the headaches of using different low level protocols. Interconnectors between modules will be easily detached and reattached.  

### Logical Topology

Logical Topology closely follows Physical Topology as it is also a star; one master MCU connects master (Mainframe) to internal pheripherals and manages dataflow.
In future versions a handshake protocol may be implemented to make configuration easier.

## Mainframe - Main MCU communication

Modularity is achieved by designating as many tasks and functions as close to physical effectors and sensors as possible. 
This dictates that Mainframe-MCU communication needs to transport as high level instrucions as possible but enough for robot to unambiguously determine desired state and for mainframe to determine actual state.

To ensure fast and robust communication Main MCU will buffer all incoming data and if there won't be update, retransfer it as required.

Master sends Desired State from Nodes to execute or master Requests Actual State from Nodes for master to acquire and process it.

## Data Stored and Processed
**Accesible by master**, _Planned_. All informations shown below are desired to be actual if open close loop control is used.  

#### by Arm MCU

* Arm servo position
* Clamp servo position
* **Arm cartesian position**
* _Arm cartesian orientation_
* **Clamp state**

#### by Chassis MCU

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
1. Communication needs to be bidirectional.
2. To ease implementation there will be a ladder of master hierarchy: Mainframe -> Main MCU -> Module MCU.
3. Main MCU will be managing all traffic and all possible low level protocol transitions.
4. All communication will use ONE encapsulation and command set.
5. Each element of network will store and process data necessary to properly execute dedicated functions. 
