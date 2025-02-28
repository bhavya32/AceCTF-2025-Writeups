# Exploiting PHP Type Juggling in Web Exploitation Challenge  

## Challenge Analysis  

The objective of this challenge is to exploit **PHP's type juggling and array handling** to bypass an **MD5 hash comparison**.  

### Given Conditions  
1. The values of `tom` and `jerry` must be different:  
``   $_GET['tom'] != $_GET['jerry']``


2. The MD5 hash of ACECTF concatenated with tom must be loosely equal (==) to the MD5 hash of ACECTF concatenated with jerry:
``md5('ACECTF' . $_GET['tom']) == md5('ACECTF' . $_GET['jerry'])``

**Key Exploit Insight**
In PHP, when an array is concatenated with a string, it is converted into the string "Array".
If tom and jerry are both arrays, they will resolve to "ACECTFArray", resulting in identical MD5 hashes.
Even though the hashes match, PHP still treats two different arrays as distinct, satisfying the condition that tom != jerry.

To exploit this behavior, we send tom and jerry as arrays with different values:
``https://chal.acectf.tech/Webrypto/?tom[]=a&jerry[]=b``
