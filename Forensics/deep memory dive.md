**🛡️ ACECTF | Deep Memory Dive 🛡️**

**🔍 Challenge Overview:**  
A gamer noticed unusual behavior in their system startup registry. The task was to analyze a **memory dump** and retrieve the hidden flag, which was split into multiple parts.  

---

**🛠️ Solution Steps:**  

1️⃣ **Searching for Readable Flag Parts**  
   - Opened the memory dump in **Notepad** and searched for **`ACECTF{`**.  
   - Found a large portion of the flag embedded in the memory.

2️⃣ **Extracting Files from Memory**  
   - Used **Volatility Workbench** to perform a **filescan**:  
     ```bash
     volatility -f memory_dump.raw --profile=Win10x64_19041 filescan
     ```
   - Located a suspicious executable file:  
     ```
     \Desktop\last_part_is_{r1ddl3s}.exe.exe
     ```
   - The filename contained the **final portion of the flag**.

3️⃣ **Reconstructing the Flag**  
   - Combined all extracted flag segments into the final format.

---

🏆 **Final Flag:**  ACECTF{retrieved_memory_r1ddl3s}