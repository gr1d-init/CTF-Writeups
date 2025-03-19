![](./assets/question.png)  
---
### Goals
1. To detect malware sample with YARA rule while avoiding false positives and false negatives.
2. Malware can exist in packed(obfuscated) or unpacked(fully extracted in memory), the rule should cover both version.
---
### Solution:

```
rule suspacked
{
    strings:
        $packed_div = ".text$div"

    condition:
        all of them
}

rule susunpacked
{
    strings:
        $unpacked_xml = "<?xml version='1.0' encoding='UTF-8' standalone='yes'?>"
        $unpacked_dll = "ADVAPI32.dll"

    condition:
        all of them
}
```  
1. Search for yara rule, follow the hint given, work with the format:
https://yara.readthedocs.io/en/stable/writingrules.html
2. Open file with ghidra, search for strings, do trial and error
### Final Result
---
**Flag:** `picoCTF{yara_rul35_r0ckzzz_74c37bd8}`
