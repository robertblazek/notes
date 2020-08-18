---
title: Terminal server and BYOD investigations
created: '2020-06-30T14:29:26.395Z'
modified: '2020-07-04T08:46:03.614Z'
---

# Terminal server and BYOD investigations

## RDP clients
- Built-in Microsoft RDP client on Windows works well
- Official MS RDP client on Mac doesn't pass through the microphone. Working Mac alternative – RoyalTSx (freeRDP on the backend)
- Linux – freeRDP standalone
## Swyx/NetPhone Client
- Audio over RDP session _"isn't supported"_. Other SIP clients perfectly support it and just use `Remoteaudio` as a default audio device. Client recommendation – Jitsi
- Swyx server doesn't work with other SIP clients __when NetPhone isn't logged in__. When it is, other clients work just fine.
