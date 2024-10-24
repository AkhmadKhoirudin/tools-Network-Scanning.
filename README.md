# tools-Network-Scanning.

Teknik yang kamu gunakan untuk memeriksa perangkat-perangkat yang terhubung ke jaringan disebut Network Scanning. Ada beberapa sub-kategori dari teknik ini, tergantung pada alat dan metode yang digunakan:

  1.  Ping Sweep (ICMP Sweep): Ini adalah teknik yang digunakan untuk mengirimkan paket ICMP (ping) ke beberapa alamat IP dalam jaringan untuk mengetahui mana yang aktif. Contoh alat yang digunakan untuk ini adalah nmap dan fping.

   2. ARP Scanning: Teknik ini memanfaatkan protokol ARP (Address Resolution Protocol) untuk menemukan perangkat di jaringan lokal. ARP scan digunakan untuk memetakan alamat IP ke alamat MAC. Contoh alat yang digunakan untuk ini adalah arp-scan.
   3. Host Discovery: Ini adalah teknik umum dalam network scanning yang bertujuan menemukan perangkat aktif di jaringan. Host discovery bisa dilakukan dengan berbagai alat seperti nmap, netdiscover, atau fping.

   Network Mapping: Teknik ini melibatkan pemetaan seluruh perangkat yang ada di jaringan, termasuk informasi seperti IP, MAC address, dan nama host.

# contoh penerapanya 

 
  1.Ping Sweep dengan nmap

Teknik ini digunakan untuk menemukan perangkat aktif di jaringan dengan mengirimkan paket ICMP (ping).
````
sudo nmap -sn 192.168.1.0/24

````

dengan output contoh 
````
┌──(udi㉿192)-[~]
└─$ sudo nmap -sn 192.168.1.0/24

Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-24 19:20 HKT
Nmap scan report for gpon.net (192.168.1.1)
Host is up (0.00060s latency).
MAC Address: E4:66:AB:A4:EF:EA (zte)
Nmap scan report for 192.168.1.2 (192.168.1.2)
Host is up (0.0011s latency).
MAC Address: 6C:F0:49:70:EE:CE (Giga-byte Technology)
Nmap scan report for 192.168.1.9 (192.168.1.9)
Host is up (0.038s latency).
MAC Address: 5E:3F:64:AB:C7:59 (Unknown)
Nmap scan report for 192.168.1.4 (192.168.1.4)
Host is up.
Nmap scan report for 192.168.1.6 (192.168.1.6)
Host is up.
Nmap done: 256 IP addresses (5 hosts up) scanned in 2.11 seconds
                                                                      
````
2.ARP Scanning dengan arp-scan

Teknik ini memanfaatkan protokol ARP untuk memetakan alamat IP ke alamat MAC di jaringan lokal.

````
sudo arp-scan --interface=<interface> 192.168.1.0/24


````

Penjelasan:

   Ganti <interface> dengan nama antarmuka jaringan yang kamu gunakan, seperti (eth0) untuk kabel atau (wlan0) untuk Wi-Fi.
   192.168.1.0/24 adalah rentang jaringan lokal.
    
 contoh output:
 ````
─(udi㉿192)-[~]
└─$ sudo arp-scan --interface=eth0 192.168.1.0/24 

Interface: eth0, type: EN10MB, MAC: 28:d2:44:9d:60:6a, IPv4: 192.168.1.4
WARNING: Cannot open MAC/Vendor file ieee-oui.txt: Permission denied
WARNING: Cannot open MAC/Vendor file mac-vendor.txt: Permission denied
Starting arp-scan 1.10.0 with 256 hosts (https://github.com/royhills/arp-scan)
192.168.1.1     e4:66:ab:a4:ef:ea       (Unknown)
192.168.1.2     6c:f0:49:70:ee:ce       (Unknown)
192.168.1.9     5e:3f:64:ab:c7:59       (Unknown: locally administered)
192.168.1.5     8a:c6:79:7c:a8:9e       (Unknown: locally administered)

4 packets received by filter, 0 packets dropped by kernel
Ending arp-scan 1.10.0: 256 hosts scanned in 1.846 seconds (138.68 hosts/sec). 4 responded
                                                                                 
┌──(udi㉿192)-[~]
└─$ sudo arp-scan --interface=wlan0 192.168.1.0/24

Interface: wlan0, type: EN10MB, MAC: e8:2a:ea:83:1a:bc, IPv4: 192.168.1.6
WARNING: Cannot open MAC/Vendor file ieee-oui.txt: Permission denied
WARNING: Cannot open MAC/Vendor file mac-vendor.txt: Permission denied
Starting arp-scan 1.10.0 with 256 hosts (https://github.com/royhills/arp-scan)
192.168.1.1     e4:66:ab:a4:ef:ea       (Unknown)
192.168.1.2     6c:f0:49:70:ee:ce       (Unknown)

2 packets received by filter, 0 packets dropped by kernel
Ending arp-scan 1.10.0: 256 hosts scanned in 1.856 seconds (137.93 hosts/sec). 2 responded
                                                                      
````

# 3. Network Discovery dengan netdiscover
  Teknik ini digunakan untuk menemukan perangkat-perangkat yang terhubung di jaringan dengan memantau lalu lintas ARP.
````
sudo netdiscover -r 192.168.1.0/24

````
Penjelasan:

   -r digunakan untuk menentukan rentang jaringan yang ingin dipindai.
   192.168.1.0/24 adalah rentang IP dari 192.168.1.1 hingga 192.168.1.254.

contoh hasil 
````
 Currently scanning: Finished!   |   Screen View: Unique Hosts                  
                                                                                
 6 Captured ARP Req/Rep packets, from 6 hosts.   Total size: 360                
 _____________________________________________________________________________
   IP            At MAC Address     Count     Len  MAC Vendor / Hostname      
 -----------------------------------------------------------------------------
 192.168.1.1     e4:66:ab:a4:ef:ea      1      60  zte corporation              
 192.168.1.2     6c:f0:49:70:ee:ce      1      60  GIGA-BYTE TECHNOLOGY CO.,LTD.
 192.168.1.9     5e:3f:64:ab:c7:59      1      60  Unknown vendor               
 192.168.1.5     8a:c6:79:7c:a8:9e      1      60  Unknown vendor               
 192.168.1.4     e8:2a:ea:83:1a:bc      1      60  Intel Corporate              
 192.168.1.6     e8:2a:ea:83:1a:bc      1      60  Intel Corporate              
         
````

  
