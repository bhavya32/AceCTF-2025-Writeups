Writeup: Hidden in the Traffic (ACECTF)
🔍 Challenge Overview

We intercepted network traffic and needed to analyze it to extract a hidden flag. The provided file was a PCAPNG capture, and the challenge hint suggested that the data might be hidden within ICMP traffic.
🛠️ Solution Approach

    Analyze the PCAP file using tshark
    We first listed ICMP payloads to check for hidden patterns:

tshark -r Very_mysterious_file.pcapng -Y "icmp" -T fields -e data.data

This revealed a repeating hex pattern.

Extract and clean the data
We concatenated all the hex values into a single string for further processing:

tshark -r Very_mysterious_file.pcapng -Y "icmp" -T fields -e data.data | tr -d '\n'

Convert Hex to ASCII
Converting the extracted hex payloads to readable ASCII:

tshark -r Very_mysterious_file.pcapng -Y "icmp" -T fields -e data.data | tr -d '\n' | xxd -r -p

Output:

ACECTF{p1n6_0f_D347h}
