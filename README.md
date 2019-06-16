# WakeOnLan
Arduino Wake On Lan ( ESP8266 &amp; ESP32 )

## **Install**


#### Include and initialize WiFiUDP
```
#include <WiFiUDP.h>
WiFiUDP UDP;
```

#### Include and initialize WakeOnLan class
```
#include "WakeOnLan.h"
WakeOnLan WOL(UDP);
```

#### Add this line in void setup() (Optinal)

```
WOL.setBroadcastAddress(WiFi.broadcastIP());
WOL.setRepeat(3, 100); // Repeat three times with 100ms delay between
```
  
## **Usage: send WOL**  

#### Set MAC address in variable
```
uint8_t MAC[6] = {0x01, 0x23, 0x45, 0x67, 0x89, 0xAB}; // 01:23:45:67:89:AB
```

##### Send WOL UDP packet (By default port 9)
`WOL.sendMagicPacket(MAC, sizeof(MAC));`

##### Send WOL UDP packet (Use port 7)
`WOL.sendMagicPacket(MAC, sizeof(MAC), 7);`


#### Set MAC address and SecureOn in variable
```
uint8_t MAC[6] = {0x01, 0x23, 0x45, 0x67, 0x89, 0xAB}; // 01:23:45:67:89:AB
uint8_t SECURE_ON[6] = {0xFE, 0xDC, 0xBA, 0x98, 0x76, 0x54}; // FE:DC:BA:98:76:54
```

##### Send WOL UDP packet with password (By default port 9)
`WOL.sendSecureMagicPacket(MAC, sizeof(MAC), SECURE_ON, sizeof(SECURE_ON));`

##### Send WOL UDP packet with password (Use port 7)
`WOL.sendSecureMagicPacket(MAC, sizeof(MAC), SECURE_ON, sizeof(SECURE_ON), 7);`


## **Usage: generate WOL**  

#### Generate
```
size_t magicPacketSize = 6 + (6 * 16);  // FF*6 + MAC*16
uint8_t* magicPacket = new uint8_t[magicPacketSize]; // Magic packet will be stored in this variable

uint8_t MAC[6] = {0x01, 0x23, 0x45, 0x67, 0x89, 0xAB}; // 01:23:45:67:89:AB

WOL.generateMagicPacket(magicPacket, magicPacketSize, pMacAddress, sizeof(MAC));
```

#### Generate with secure on
```
size_t magicPacketSize = 6 + (6 * 16) + 6;  // FF*6 + MAC*16 + SecureOn
uint8_t* magicPacket = new uint8_t[magicPacketSize]; // Magic packet will be stored in this variable

uint8_t MAC[6] = {0x01, 0x23, 0x45, 0x67, 0x89, 0xAB}; // MAC Address = 01:23:45:67:89:AB
uint8_t SECURE_ON[6] = {0xFE, 0xDC, 0xBA, 0x98, 0x76, 0x54}; // SecureOn = FE:DC:BA:98:76:54

WOL.generateMagicPacket(magicPacket, magicPacketSize, MAC, sizeof(MAC), SECURE_ON, sizeof(SECURE_ON));
```
