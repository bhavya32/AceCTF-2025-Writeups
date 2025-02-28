# Hidden in the Traffic  

**Category:** Network Forensics  

The challenge involves analyzing intercepted **network traffic** to uncover a **hidden message** within a **PCAPNG file**. Based on the challenge description, the secret communication is embedded in **ICMP traffic** (often associated with ping requests and replies).  

---

### Challenge  

**Provided File:** `Very_mysterious_file.pcapng`  

---

## Overview  

1. **Analyze the PCAP File**  
   - Open the file using **tshark** to inspect the traffic patterns.  
   - Look for unusual ICMP messages that may contain hidden data.  

2. **Extract ICMP Payloads**  
   - Use `tshark` to filter out **ICMP** packets and extract their payload data:  
     ```bash
     tshark -r Very_mysterious_file.pcapng -Y "icmp" -T fields -e data.data
     ```  
   - This reveals a sequence of **hex-encoded** data embedded within ICMP packets.  

3. **Concatenate and Convert Hex to ASCII**  
   - Remove newline characters to obtain a continuous hex string:  
     ```bash
     tshark -r Very_mysterious_file.pcapng -Y "icmp" -T fields -e data.data | tr -d '\n'
     ```  
   - Convert the extracted hex data into readable ASCII text:  
     ```bash
     tshark -r Very_mysterious_file.pcapng -Y "icmp" -T fields -e data.data | tr -d '\n' | xxd -r -p
     ```  

---

### Final Flag  

After decoding the ICMP payload data, the extracted flag is:  

```
ACECTF{p1n6_0f_D347h}
```
