# BWCH

BWCH stands for **B**o**w**ling **Ch**allenge, and contains data for stages used in the bowling training games of *Wii Sports* (not counting Power Throws as it is hardcoded).   
Both Picking Up Spares and Spin Control both use BWCH files, meaning that you *could* place gates in Picking Up Spares.  
Each stage only supports up to 10 pins and 15 gates, however the BWCH format seems to be able to specify the amount of stages that exist within the file,
even though *Wii Sports* is hardcoded to load a certain amount.  

## Structure

### Header  
Each BWCH file begins with a `0x44 (52)` byte header, structured as follows:

| **Offset** | **Size** | **Type** | **Description** |
|------------|---------|----------|-----------------|
|0x00|0x04|char[4]|File magic (always `BWCH`)|
|0x04|0x04|u32|Unknown, possibly build date string length / 0x10?|
|0x08|**L**|string|BWCH build date of length **L** (specified above)|
|0x08 + **L**|0x04|u32|Unknown value (maybe offset?)|
|0x0C + **L**|0x04|u32|Unknown value (maybe offset?)|
|0x10 + **L**|0x04|u32|Stage count|
  
  
### Stage  
The header is followed by X stages, with X representing the stage count u32 in the header.

| **Offset** | **Size** | **Type** | **Description** |
|------------|---------|----------|-----------------|
|0x00|0x100|Gate[16]|Gate data for gates 0-15|
|0x100|0x50|Pin[10]|Pin data for pins 0-9|

#### Gate
The data for a gate consists of a few variables:  

| **Offset** | **Size** | **Type** | **Description** |
|------------|----------|----------|-----------------|
|0x00|0x04|single|Gate X size (length)|
|0x04|0x04|single|Unknown value|
|0x08|0x04|single|Gate X position (relative to bowling lane)|
|0x0C|0x04|single|Gate Z position (relative to bowling lane)|  
  
#### Pin
The data for a pin consists of seemingly obfuscated boolean values:  

| **Offset** | **Size** | **Type** | **Description** |
|------------|----------|----------|-----------------|
0x00|0x08|single[2]|Pin status. Both must be greater or equal to `-1000f` for the pin to show. If at least one of the singles is less than `-1000f`, the pin will not appear.|  
  
    
**Thanks to KILL043/GibHaltmannKill for doing the reverse engineering work necessary to obtain this reference material.**  
  
  
## Tools that can edit BWCH  

[Spin Controller](./tools/BWCH/SpinController.exe) by KILL043/GibHaltmannKill



[Back to Formats](formats.md)
