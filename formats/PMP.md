# PMP

PMP files are used across many *Wii* series games, and even saw an appearance in *Wii Party U*, which came out more than 5 years (a console generation) after the format was developed.  
It is believed PMP stands for **P**ack **M**a**p** (*Wii Sports*' codename being "Sports **Pack** for Revolution").  
PMP files store data for object arrangement in 3D space, and has 3 main components: objects, routes, and points.  
Routes are composed of points, and objects are commonly configured via game logic to animate across routes.  
PMP objects are also useful for models that are used in many places (common assets), so they don't have to be included in the environment model.

## Structure

### Header  
Each PMP file begins with a header, structured as follows:

| **Offset** | **Size** | **Type** | **Description** |
|------------|---------|----------|-----------------|
|0x00|0x04|char[4]|File magic (always `PMPF`)|
|0x10|0x02|u16|Object count|
|0x12|0x02|u16|Route count|
|0x14|0x02|u16|Point count|
|0x40|0x04|u32|Object data offset|
|0x44|0x04|u32|Route data offset|
|0x48|0x04|u32|Point data offset|
  
  
### Object Data

| **Offset** | **Size** | **Type** | **Description** |
|------------|---------|----------|-----------------|
|0x00|0x02|u16|Group ID|
|0x02|0x02|u16|Object ID|
|0x04|0x04|u32|Unknown|
|0x08|0x0C|single[3]|Position vector|
|0x14|0x0C|single[3]|Scaling vector|
|0x20|0x0C|single[3]|Transformation matrix (first column)|
|0x2C|0x0C|single[3]|Transformation matrix (second column)|
|0x38|0x0C|single[3]|Transformation matrix(third column)|
|0x44|0x04|u32|Unknown|
|0x48|0x10|varies|Object-specific parameters|

### Route Data

| **Offset** | **Size** | **Type** | **Description** |
|------------|----------|----------|-----------------|
|0x00|0x02|u16|Point count|
|0x02|0x04|u32|Unknown|
|0x06|0x02|u16|Route group ID|
|0x08|0x12|string|Internal route name (if applicable)|
|0x1A|0x02|u16|Route point index|
|0x1C|0x05|u32|Unknown|
  
### Point Data

| **Offset** | **Size** | **Type** | **Description** |
|------------|----------|----------|-----------------|
|0x00|0xC|single[3]|Position vector|
|0x0C|0x08|varies|Additional parameters|  
  
  
**Thanks to KILL043/GibHaltmannKill and [JimmyKaz](https://www.youtube.com/channel/UCUplC9g5Clc2PLr293HDPUA) for doing the reverse engineering work necessary to obtain this reference material.**  
  
  
## Tools that can edit PMP  

[PMP Editor](/tools/PMP/PMPEditor.exe) by KILL043/GibHaltmannKill and [JimmyKaz](https://www.youtube.com/channel/UCUplC9g5Clc2PLr293HDPUA)



[Back to Formats](formats.md)
