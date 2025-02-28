# Broken Secrets  

**Category:** Forensics  

The challenge involves analyzing a **broken file** that cannot be opened normally. The objective is to uncover its secrets by investigating its structure, extracting hidden files, and repairing any corruption.  

---

### Challenge  

**Provided File:** `Brokenfr`  

---

## Overview  

1. **Extracting the Archive**  
   - Attempt to extract the contents using a tool like **7-Zip**:  
     ```bash
     7z x Brokenfr
     ```  
   - Look for any suspicious files inside the extracted folders.  

2. **Identifying the Suspicious File**  
   - The file was found inside:  
     ```
     word/media/
     ```
   - Name of the file:  
     ```
     not_so_suspicious_file
     ```

3. **Analyzing the File Type**  
   - Use `xxd` to check its contents and detect its format:  
     ```bash
     xxd not_so_suspicious_file | head
     ```  
   - The header appears **corrupted**, preventing normal access.

4. **Fixing the Corrupted Header**  
   - Identify the **correct PNG header** and replace it.  
   - Use a hex editor (e.g., `hexedit` or `bless`) to modify the file.  

5. **Opening the Image**  
   - After fixing the header, open the image to retrieve the hidden flag.  

---

### Final Flag  

After extracting and repairing the image, the revealed flag is:  

```
ACECTF{h34d3r_15_k3y}
```
