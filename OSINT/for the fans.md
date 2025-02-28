🔍 **Searching for the Account**  
- Look up **"DrakeSaltyOVO"** on **X (formerly Twitter)** to find the account.  
- Once found, extract the **username** and use it for further investigation.  

🕵️ **Google Dorking for Hidden Blog**  
- Use **Google dorks** with the username to locate **personal blogs or archives**:  
  ```bash
  site:pastebin.com OR site:medium.com OR site:wordpress.com "DrakeSaltyOVO"
  ```  
- A blog containing **a suspicious encoded string** is found.  

🔐 **Decoding the Hidden File**  
- Copy the **encoded string** into **CyberChef** and decode it as **Base64**.  
- The decoded output reveals a **7z (7-Zip) archive file**.  

🔑 **Extracting the Archive**  
- Attempt to extract the **7z file**, but it prompts for a **password**.  
- Return to the **X profile**—a post suggests the password format includes the **birth date**.  
- Use the **birth date** as the **7z password** and successfully extract the flag.
