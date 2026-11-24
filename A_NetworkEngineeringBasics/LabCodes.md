# Lab Codes
## Ders 1
- MacOs sisteminde IP adresi ve MAC adresini verir.
```bash
ifconfig en0
```
	ether x8:80:xx:xx:xx:xx 
	inet 192.168.1.xx

- Ağ üzerinde bulunan cihazların IP adresini verir. 
```bash
arp - a
```
	? (192.168.1.1) at xx:xx:xx:xx:xx:xx on en0 ifscope [ethernet] 
	? (192.168.1.131) at xx:xx:xx:xx:xx:xx on en0 ifscope [ethernet] 
	? (192.168.1.143) at xx:xx:xx:xx:xx:xx on en0 ifscope [ethernet] 
	? (192.168.1.151) at xx:xx:xx:xx:xx:xx on en0 ifscope [ethernet] 
	? (192.168.1.157) at xx:xx:xx:xx:xx:xx on en0 ifscope [ethernet] 
	? (192.168.1.178) at xx:xx:xx:xx:xx:xx on en0 ifscope permanent [ethernet] 
	? (192.168.1.198) at xx:xx:xx:xx:0:xx on en0 ifscope [ethernet] 

- Bir websitesi yada sunucuya IP üzerinden erişim kontrolü yapar. 
```bash
ping -c 4 1.1.1.1
```
	PING 1.1.1.1 (1.1.1.1): 56 data bytes 64 bytes from 1.1.1.1: icmp_seq=0 ttl=45 time=79.160 ms 
	--- 1.1.1.1 ping statistics 
	--- 1 packets transmitted, 1 packets received, 0.0% packet loss round-trip 
	min/avg/max/stddev = 79.160/79.160/79.160/0.000 ms

- Sitenin yada IP nin port erişim kontrolünü yapar. 
```bash
nc -nc -zv example.com 443
```
	Connection to example.com port 443 [tcp/https] succeeded!

- MacOs sisteminde dinlenen portları listeler.
```bash
sudo lsof -iTCP -sTCP:LISTEN -n -P | head -15
```
	COMMAND PID USER FD TYPE DEVICE SIZE/OFF NODE NAME launchd 
	1 root 21u IPv6 xx 0t0 TCP *:445 (LISTEN) launchd 
	1 root 22u IPv4 xx 0t0 TCP *:445 (LISTEN) launchd 
	1 root 24u IPv6 xx 0t0 TCP *:445 (LISTEN) launchd

## Ders 2

- Veri paketi yolunu takip eder.
```bash
traceroute -n 1.1.1.1
``` 
	traceroute to 1.1.1.1 (1.1.1.1), 64 hops max, 40 byte packets 
	1 192.168.1.1 1.043 ms 0.596 ms 0.485 ms 
	2 * * * 
	3 172.19.7.97 56.873 ms 21.704 ms 20.880 ms 
	4 172.16.197.173 19.096 ms 21.886 ms 24.949 ms

- Network bağlantı testi
```bash
networkQuality
```
	Downlink: 1.058 Mbps, 76 RPM - Uplink: 13.199 Mbps, 76 RPM

## Ders 3

- Router varsayılan ağ geçidini verir. 
```bash
netstat -rn | grep default
```
	default  192.168.1.1 UGScg en0

- Cihazdaki ağ arabirimlerini listeler. 

```bash
networksetup -listallhardwareports
```
	Hardware Port: Ethernet Device: 
	en0 Ethernet Address: xx:xx:xx:xx:xx:xx

- Wifi bağlantı kalitesi bilgisini sağlar. 

```bash
system_profiler SPAirPortDataType | grep -A 12 "Current Network Information"
```
	Current Network Information: <redacted>: 
	PHY Mode: 802.11ax Channel: 100 (5GHz, 80MHz) 
	Country Code: TR Network Type: Infrastructure 
	Signal / Noise: -32 dBm / -92 dBm 
	Transmit Rate: 1200 MCS Index: 1

## Ders 4

- ARP'in IP yakalaması
```bash
sudo tcpdump -i en0 -n arp -c 4
```
	07:10:04.419431 ARP, Request who-has 192.168.1.178 tell 192.168.1.151
	07:10:04.419510 ARP, Reply 192.168.1.178 is-at xx:xx:xx:xx:xx:xx, length 28 
	07:10:05.382866 ARP, Request who-has 192.168.1.140 (ff:ff:ff:ff:ff:ff) tell 192.168.1.1

- Port numaralarının resmî isimleri
```bash
grep -E "^(ssh|http|https|domain|ntp|smtp)[[:space:]]" /etc/services | head -12
```

	ssh 22/udp # SSH Remote Login Protocol 
	ssh 22/tcp # SSH Remote Login Protocol 
	smtp 25/udp # Simple Mail Transfer 
	smtp 25/tcp # Simple Mail Transfer 
	domain 53/udp # Domain Name Server 
	domain 53/tcp # Domain Name Server 
	http 80/udp www www-http # World Wide Web HTTP 
	http 80/tcp www www-http # World Wide Web HTTP 
	ntp 123/udp # Network Time Protocol 
	ntp 123/tcp # Network Time Protocol 
	https 443/udp # http protocol over TLS/SSL 
	https 443/tcp # http protocol over TLS/SSL

- Protokol kontrol ve cevap alınması
```bash
curl -sv http://example.com -o /dev/null 2>&1 | head -15
```

	* Host example.com:80 was resolved. 
	* IPv6: 2606:4700:10::ac42:93f3, 2606:4700:10::6814:179a 
	* IPv4: 172.66.147.243, 104.20.23.154 * Trying [2606:4700:10::ac42:93f3]:80... 
	* Connected to example.com (2606:4700:10::ac42:93f3) port 80
	* GET / HTTP/1.1 > 
	* Host: example.com > 
	* User-Agent: curl/8.7.1 > Accept: */*  
	* Request completely sent off 
	* < HTTP/1.1 200 OK

-  Birden çok portu test etdilmesi
```bash
nc -zv -w 3 example.com 80 443 22
```
	* Connection to example.com port 80 [tcp/http] succeeded!

- Site DNS'i hangi portu kullanıyor. 
```bash
dig example.com | grep -E "SERVER|ANSWER SECTION" -A1
```
	* ANSWER SECTION: 
	* example.com. 202 IN A 172.66.147.243

## Ders 5

- Katmanların test edilmesi
```bash
ifconfig en0 | grep status # Katman 1 Testi
```
```bash
 status: active
```
---
---

```bash
arp -a # Katman 2 Testi
```
```bash
ipad-8.local (169.254.214.181) at (incomplete) on en9 [ethernet]
? (192.168.1.1) at xx:xx:xx:xx:xx:xx on en0 ifscope [ethernet]
? (192.168.1.131) at xx:xx:xx:xx:xx:xx on en0 ifscope [ethernet]
```
---
---
```bash
ping -c 4 127.0.0.0     # Katman 3 Testi    (PC IP SONUCU)
ping -c 4 192.168.1.1   # Katman 3 Testi    (ROUGTER IP SONUCU)
ping -c 4 1.1.1.1       # Katman 3 Testi    (SUNUCU IP SONUCU)
```
```bash

--- 127.0.0.0 ping statistics ---
4 packets transmitted, 0 packets received, 100.0% packet loss
PING 192.168.1.1 (192.168.1.1): 56 data bytes
64 bytes from 192.168.1.1: icmp_seq=0 ttl=64 time=0.866 ms
64 bytes from 192.168.1.1: icmp_seq=1 ttl=64 time=0.791 ms
64 bytes from 192.168.1.1: icmp_seq=2 ttl=64 time=0.909 ms
64 bytes from 192.168.1.1: icmp_seq=3 ttl=64 time=0.815 ms

--- 192.168.1.1 ping statistics ---
4 packets transmitted, 4 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 0.791/0.845/0.909/0.046 ms
PING 1.1.1.1 (1.1.1.1): 56 data bytes
64 bytes from 1.1.1.1: icmp_seq=0 ttl=44 time=116.680 ms
64 bytes from 1.1.1.1: icmp_seq=1 ttl=44 time=87.751 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=44 time=83.140 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=44 time=97.107 ms

--- 1.1.1.1 ping statistics ---
4 packets transmitted, 4 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 83.140/96.169/116.680/12.867 ms
```
---
---
```bash
nc -zv -w 3 example.com 443 # Katman 4 Testi (Port Testi)
```
```bash

Connection to example.com port 443 [tcp/https] succeeded!

```
---
---
```bash
dig tshort example.com  # Katman 7 Testi
curl -sI https://example.com | head -3 
```
```bash

;; ANSWER SECTION:
example.com.            225     IN      A       172.66.147.243
example.com.            225     IN      A       104.20.23.154

;; Query time: 15 msec
;; SERVER: 192.168.1.1#53(192.168.1.1)
;; WHEN: Tue Nov 24 14:21:37 +03 2026
;; MSG SIZE  rcvd: 72

HTTP/2 200
date: Tue, 24 Nov 2026 11:21:38 GMT
content-type: text/html; charset=utf-8

```
