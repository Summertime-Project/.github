# Data Frame

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
|5| MNR0| 3bit number of module, may be somewhat redundant|
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
(Online CRCcalc?) [https://crccalc.com/]

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
BIG ENDIAN!!!!!!!

#### Data
|V1 | LEN | INT | intLEN | 0byte | 1byte | 2byte | 3byte | INT | intLEN | 0byte | 1byte | 2byte | 3byte | INT | intLEN | 0byte | 1byte | 2byte | 3byte |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| C1 | 12 | 02 | 4 | 00 | D0 | 11 | 01 | 02 | 4 | 00 | D0 | 11 | 01 | 02 | 4 | 00 | 00 | 00 | 00 |

### Big enc
| CONF | BODY | CRC |
|---   |---   |---  |
|01  | BODY | 53 |


