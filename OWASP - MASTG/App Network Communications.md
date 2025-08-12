---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/owasp-mastg/app-network-communications/"}
---






# ==Simulating MiTM with bettercap==

```Shell
sudo bettercap -eval "set arp.spoof.targets X.X.X.X; arp.spoof on; set arp.spoof.internal true; set arp.spoof.fullduplex true;"
```

- On the mobile phone start the browser and navigate to http://example.com, you should see output like the following when you are using Wireshark.

# ==With AP==

- Perform the following on Kali with configured APs to your host computer

```Shell
# check if other process is not using WiFi interfaces
$ airmon-ng check kill
# configure IP address of the AP network interface
$ ifconfig wlan1 10.0.0.1 up
# start access point
$ hostapd hostapd.conf
# connect the target network interface
$ wpa_supplicant -B -i wlan0 -c wpa_supplicant.conf # run DNS server
$ dnsmasq -C dnsmasq.conf -d
# enable routing
$ echo 1 > /proc/sys/net/ipv4/ip_forward
# iptables will NAT connections from AP network interface to the target network interface $ iptables --flush
$ iptables --table nat --append POSTROUTING --out-interface wlan0 -j MASQUERADE
$ iptables --append FORWARD --in-interface wlan1 -j ACCEPT
$ iptables -t nat -A POSTROUTING -j MASQUERADE
```

- Analyse traffic through Wireshark and/or tcpdump

# ==Proxy Runtime Instrumentation==

## ==Dealing with Xamarin Apps==

- Add a default proxy to the app, by adding the following code in the OnCreate or Main method and re-create the app:

```Shell
WebRequest.DefaultWebProxy = new WebProxy("192.168.11.1", 8080);
```

- Tweaking the /etc/hosts on the mobile phone. Add an entry into /etc/hosts for the target domain and point it to the IP address of your intercepting proxy.
    - This creates a similar situation of being MITM as with bettercap and you need to redirect port 443 to the port which is used by your interception proxy.
    - Additionally, you need to redirect traffic from your interception proxy to the original location and port (Burp).