# Data Frame

# Structure 
## Big encapsulation
Big encapluation task is to provide direct and errorless Body transfer between nodes.

|CONF - 1| BODY - LEN | CRC - 1|
|---|---|---|
    
### CONF
If RFU then should be set to 0.

|bit |Short |Desc |
|--- |---- |---- |
|0| RFU||
|1| RFU||
|2| RFU||
|3| RFU||
|4| RFU||
|5| MNR0| 3bit number of module|
|6| MNR1||
|7| MNR2||

|MNR| Module|
|---|---|
|0| Main (sholud not used)|
|1| Chassis|
|2| Arm|
|3| Cam Turret|
|4| Prox|

### BODY

TLV encapsulated Data, before encapsulation refactor all datatypes to Network(Big) Endian

### CRC
One byte CRC wil be derrived from LEN and BODY
(Online CRCcalc?) [https://crccalc.com/]

## DER-TLV Encapsulation

[Der-TLV](https://www.oss.com/asn1/resources/asn1-made-simple/asn1-quick-reference/basic-encoding-rules.html)

### Private Tags

#### Primitive
|Num |Name |Desc |Simillar Type |
|--- |---- |---- |---- |
|0| REQUEST| requests data from slave, in Value should be requested tag| UINT16|
|1| RFU| | |
|2| ARC| Arm's Clamp Open/Closed| BOOL(DER???     FF=True, 00=False, else error?)|

#### Constructed
|Num |Name |Desc | Containing|
|--- |---- |---- | ----------|
|00| ALL| All available data transfered inside this tag !!!Dificult!!!| device specific|
|01| CHV| Chassis's Velocity|         3xINT32/FLOAT|
|02| CHW| Chassis's Angular velocity| 3xINT32/FLOAT|
|03| ARP| Arm's Position|         3xINT32/FLOAT|
|04| ARA| _Arm's Angle_|            3xINT32/FLOAT|
|05| PRS| Singular obstacle position| 3xINT32/FLOAT|
|06| PRM| Multiple obstacles positions| NxPRS|

## Examples

### Big enc
| CONF | BODY | CRC |
|---   |---   |---  |
|01  | BODY | 53 |

#### Data
|CH_V | LEN | INT | intLEN | 0byte | 1byte | 2byte | 3byte | INT | intLEN | 0byte | 1byte | 2byte | 3byte | INT | intLEN | 0byte | 1byte | 2byte | 3byte |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| C1 | 12 | 02 | 04 | 00 | D0 | 11 | 01 | 02 | 04 | 00 | D0 | 11 | 01 | 02 | 04 | 00 | 00 | 00 | 00 |




