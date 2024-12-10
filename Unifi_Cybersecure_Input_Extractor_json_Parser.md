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
