---
id: activegate-routing
title: ActiveGate Routing Mode Configuration
---

## ActiveGate Routing Mode Configuration

After installing the ActiveGate, you must enable the **"routing"** capability.

### 1. Edit the Configuration File

Open the `custom.properties` file located at:

`/var/lib/dynatrace/gateway/config/custom.properties`

Add the following content:

```ini
[connectivity]
dnsEntryPoint = https://[hostname.domain]:9999
```

Replace `[hostname.domain]` with your actual hostname and domain.

### 2. Restart the Service

After saving the file, restart the ActiveGate service:

```bash
sudo systemctl restart dynatracegateway
```

### Validate the Configuration
Run the following command to verify the routing endpoint:

```bash
wget https://[hostname.domain]:9999/communication
```

### Reference Documentation
https://docs.dynatrace.com/docs/ingest-from/dynatrace-activegate/configuration/set-up-reverse-proxy-for-oneagen
