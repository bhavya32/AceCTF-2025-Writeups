Writeup: Fractured Frames (ACECTF)
🔍 Challenge Overview

We received a suspicious image that had hidden information within its structure. The hint suggested that the image wasn’t erased or encoded, but rather manipulated structurally.
🛠️ Solution Approach

🔍 **Checking the Image Dimensions**  
- Use `exiftool` to inspect the metadata:  
  ```bash
  exiftool challenge.jpg
  ```  
- The **height value** appeared modified, hinting at hidden data.  

🛠 **Fixing the Image Height**  
- Adjust the **height by 1 pixel** using a **hex editor** (`hexedit`, `HXD`, or `bless`):  
  - Open the file in the hex editor.  
  - Locate the **height value** in the image header.  
  - Change **00** to **01** in the appropriate byte.  

👀 **Viewing the Fixed Image**  
- After modifying the height, the **hidden flag** became visible at the **bottom of the image**.

🏆 Final Flag

After modifying the height, the flag appeared:
```
ACECTF{th1s_sh0uld_b3_en0u6h}
```
