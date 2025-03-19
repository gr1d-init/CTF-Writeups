![](./assets/question.png)  
---
### Goals
1. The binary bininst1.exe calls the `Sleep` function from kernel32.dll
2. Using frida-trace, we generate the handler scripts for API functions
3. Intercept any call to `Sleep`, in this case, under `KERNEL32.dll`
4. We then set sleep duration to 0, avoiding the program from sleeping.
---
### Solution:
1. Using frida-trace
```bash
frida-trace -i "Sleep" ./bininst1.exe
```

2. Intercept the handler, by modifying the handler generated, changing sleep duration to zero.
```js
// KERNEL32.DLL/Sleep.js
var sleepAddr = Module.getExportByName("kernel32.dll", "Sleep");
Interceptor.attach(sleepAddr, {
    onEnter: function (args) {
        // Log the original sleep duration (for debugging)
        console.log("Original sleep time: " + args[0].toInt32());
        // Change the sleep duration to 0
        args[0] = ptr(0);
    }
});
```
### Final Result
---
**Flag:** `picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}`
