---
title: "netsh Commands"
layout: blog
topic: windows
order: 0
topic: Windows
topic_path: /docs/windows/index.html
---
Commands are tested on Powershell with admin priveleges.

Enter netsh command interface
```bash
netsh
```

Show interface
```bash
netsh interface show interface
```

Show all port proxies
```bash
netsh interface portproxy show all
```

Delete a port proxy
```bash
netsh interface portproxy delete v4tov4 listenport=3000 listenaddress:0.0.0.0
```