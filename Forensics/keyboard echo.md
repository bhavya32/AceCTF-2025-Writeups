Writeup: Keyboard Echo (ACECTF)
🔍 Challenge Overview

We intercepted USB keyboard traffic captured in a PCAPNG file, where keystrokes were encoded using the HID USB protocol. The task was to decode the captured keystrokes and reconstruct the original input.
🛠️ Solution Steps

    Extract USB Keystroke Data from the PCAP file using tshark:

tshark -r challenge.pcapng -Y "usb.capdata" -T fields -e usb.capdata >aaaa.txt

Decode the Keystroke Data:

    Each USB packet contained HID keycodes representing pressed keys.
    We mapped these codes using the HID Keyboard Keycode Table.
    The extracted raw text was:

    rrTabTaby0uh4v3f0und17arTabb

Clean the Data:

    After removing duplicates and Tab characters, the meaningful text was:

    y0uh4v3f0und17

Format the Flag according to the required structure:

ACECTF{y0uh4v3f0und17}