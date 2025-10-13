---
dg-publish: true
---






## ==Object Concatenation==

- When a compiled binary is scanned with Yara, it will create a positive alert/detection if the defined string is present.
- Using concatenation, the string can be functionally the same but will appear as two independent strings when scanned, resulting in no alerts.

```Shell
IntPtr ASBPtr = GetProcAddress(TargetDLL, "Amsi" + "Scan" + "Buffer");
```

- Extending from concatenation, attackers can also use **non-interpreted characters** to disrupt or confuse a static signature :

|   |   |   |
|---|---|---|
|Breaks|Break a single string into multiple sub strings and combine them|`('co'+'ffe'+'e')`|
|Reorders|Reorder a string’s components|`('{1}{0}'-f'ffee','co')`|
|Whitespace|Include white space that is not interpreted|`.( 'Ne' +'w-Ob' + 'ject')`|
|Ticks|Include ticks that are not interpreted|``d`own`LoAd`Stri`ng``|
|Random Case|Tokens are generally not case sensitive and can be any arbitrary case|`dOwnLoAdsTRing`|

## ==Object Names==

- Object names offer some of the most significant insight into a program's functionality and can reveal the exact purpose of a function. An analyst can still deconstruct the purpose of a function from its behavior, but this is much harder if there is no context to the function.

## ==Code Structure==

- Separation of related code can impact both interpreted and compiled languages and result in hidden signatures that may be hard to identify. A heuristic signature engine may determine whether a program is malicious based on the surrounding functions or API calls. To circumvent these signatures, an attacker can randomize the occurrence of related code to fool the engine into believing it is a safe call or function.

## ==File & Compilation Properties==

- More minor aspects of a compiled binary, such as the compilation method, may not seem like a critical component, but they can lead to several advantages to assist an analyst. For example, if a program is compiled as a debug build, an analyst can obtain all the available global variables and other program information.
- Luckily for attackers, symbol files are easily removed through the compiler or after compilation. To remove symbols from a compiler like **Visual Studio**, we need to change the compilation target from `Debug` to `Release` or use a lighter-weight compiler like **mingw.**