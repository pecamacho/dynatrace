---
id: activegate-custom-certificate
title: Configure a Custom Certificate for ActiveGate
sidebar_label: Custom Certificate ActiveGate
---
You can configure ActiveGate to serve a custom certificate instead of the default one. To configure this, you need a file in **PKCS#12 format** that contains both a **private key** and the **corresponding certificate chain**.
---

## Steps to Configure a Custom Certificate

### 1. Copy the Certificate File

Place the `.p12` certificate file in the ActiveGate SSL directory:

```bash
/var/lib/dynatrace/gateway/ssl
```

### 2. Set Proper File Permissions

Make sure the certificate file is owned by the dtuserag user and group:

```bash
chown dtuserag:dtuserag /var/lib/dynatrace/gateway/ssl/certificate-file.p12
```

### 3. Configure custom.properties
Edit the file:

```bash
/var/lib/dynatrace/gateway/config/custom.properties
```

Add or create the following section:

```ini
[com.compuware.apm.webserver]
certificate-file = certificate-file.p12
certificate-password = password
certificate-alias = friendly-name
```

### 4. Restart ActiveGate

After restarting the service, the plain-text password will be obfuscated and replaced with certificate-password-encr.

```bash
sudo systemctl restart dynatracegateway
```

### Validate the Certificate Installation

- Use curl to test communication

```bash
curl https://[hostname.domain]:9999/communication
```

Ensure there's no certificate error and the endpoint is reachable.

- Inspect Certificate with OpenSSL

```bash
openssl s_client -connect [hostname.domain]:9999
```

In the output, check the Common Name (CN) and Subject Alternative Names (SANs) to confirm that the expected internal hostname is present.

### Reference Documentation 
Dynatrace Documentation – Custom certificate for ActiveGate
https://docs.dynatrace.com/docs/ingest-from/dynatrace-activegate/configuration/configure-custom-ssl-certificate-on-activegate
