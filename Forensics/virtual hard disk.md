**🛡️ ACECTF | Alternative Secrets 🛡️**

**🔍 Challenge Overview:**  
This challenge required forensic analysis of a **disk image** to locate a hidden flag. The hint suggested that **fake flags** were placed throughout the system, making careful investigation necessary.

---

**🛠️ Solution Steps:**  

1️⃣ **Inspecting the Image with FTK Imager**  
   - Opened the provided image file using **FTK Imager**.  
   - Explored the **NTFS file system**, looking for hidden or unusual files.  
   - Found a suspicious **JPEG file** (`666c61672e747874.jpg`) containing **Alternative Data Streams (ADS)**.

2️⃣ **Extracting the Hidden Data**  
   - Noticed two ADS entries attached to the image:  
     - **Flag**
     - **Key**
   - Extracted both using FTK Imager for further analysis.

3️⃣ **Decrypting the Flag**  
   - The flag was encrypted using the **Vigenère Cipher**.  
   - Used the **key from the ADS** to decrypt the hidden text:  
     ```bash
     echo "EncryptedText" | vigenere -d -k "KeyFromADS"
     ```
   - Successfully recovered the flag.

---

🏆 **Final Flag:**  
ACECTF{7h3_d1ff3r3nc3_b37w33n_y0u_4nd_m3}