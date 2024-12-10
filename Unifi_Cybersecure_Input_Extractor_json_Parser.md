# Complete Extractor Configuration

## Step 1: Regular Expression Extractor

1. **Title**: `Unifi IPS JSON Extractor`
2. **Source Field**: `full_message`
3. **Extractor Type**: `Regular expression`
4. **Regular Expression**:
```regex
.*message queue is full, drop message: (\{.*\})$
```
5. **Configuration**:
   - Extractor Strategy: Copy
   - Target Field: `unifi_json`
   - Condition Type: Regex
   - Condition: `.*ubnt-idsips-daemon.*`

## Step 2: JSON Extractor

1. **Title**: `Unifi IPS Field Parser`
2. **Source Field**: `unifi_json`
3. **Extractor Type**: `JSON`
4. **JSON Path Specifications**:
```
alert_action           : $.alert.action
alert_category         : $.alert.category
alert_signature        : $.alert.signature
alert_severity         : $.alert.severity
alert_signature_id     : $.alert.signature_id
metadata_attack_target : $.alert.metadata.attack_target[0]
metadata_confidence    : $.alert.metadata.confidence[0]
metadata_deployment    : $.alert.metadata.deployment[0]
metadata_severity      : $.alert.metadata.signature_severity[0]
metadata_category      : $.alert.metadata.ubnt_category[0]
app_proto             : $.app_proto
dest_ip               : $.dest_ip
dest_port             : $.dest_port
dns_query             : $.dns.query[0].rrname
dns_query_type        : $.dns.query[0].rrtype
event_type            : $.event_type
src_ip                : $.src_ip
src_port              : $.src_port
protocol              : $.proto
timestamp            : $.timestamp
flow_id              : $.flow_id
input_interface      : $.in_iface
output_interface     : $.out_iface
```

## Implementation Steps:

1. Create the Regular Expression extractor first
   - Verify it successfully extracts the JSON into unifi_json field
   - Test with sample message to ensure JSON is properly captured

2. Create the JSON extractor second
   - Ensure it's ordered after the regex extractor
   - Test to verify all fields are properly extracted
  
## Example Output:

Sample Log:
```
<28>Dec 10 14:20:53 UDM-PRO-MAX UDM-PRO-MAX ubnt-idsips-daemon[311690]: 2024-12-10T14:20:53.347-0600	Warn: UploadSecurityCloud: message queue is full, drop message: {"alert":{"action":"blocked","category":"Misc activity","gid":1,"metadata":{"confidence":["High"],"created_at":["2021_06_03"],"deployment":["alert_only"],"signature_severity":["Informational"],"ubnt_category":["INFO"],"updated_at":["2023_04_28"]},"rev":4,"severity":3,"signature":"ET INFO Session Traversal Utilities for NAT (STUN Binding Request On Non-Standard High Port)","signature_id":2033078},"app_proto":"failed","dest_ip":"74.125.250.129","dest_port":19302,"dst_mac":"9e:05:d6:6f:4f:75","event_type":"alert","flow":{"bytes_toclient":0,"bytes_toserver":434,"pkts_toclient":0,"pkts_toserver":7,"start":"2024-12-10T14:20:46.903993-0600"},"flow_id":2241825332972345,"host":"usg-sensor","in_iface":"br0","out_iface":"eth8","proto":"UDP","src_ip":"10.0.0.1","src_mac":"80:61:5f:10:84:af","src_port":55912,"timestamp":"2024-12-10T14:20:53.203460-0600","ubnt":{"affected_products":"","classtype":"","counterpart_hostnames":["stun.l.google.com"],"cve_reference":"","description":"","event_version":"3.1","reference_url":[],"signature_type":"ET","ubnt_category":"INFO"}}
```
![image](https://github.com/user-attachments/assets/45274974-ef7b-459a-9050-be72c2a48d96)
