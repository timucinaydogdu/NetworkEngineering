## OSI ve TCP/IP Modelleri

1. Fiziksel Katmanı     : Bitlerin taşınması için kullanılan kablo ve jakların bağlantı katmanıdır. 

2. Veri Bağı Katmanı    : Bitlerin ağ komşu cihazları arasında teslim edilmesini sağlan bağlantı katmanıdır. 

3. Ağ Katmanı           : Ağlar arasında yönlendirme ve adresleme katmanıdır. 

4. Taşıma Katmanı       : Uçtan uca iletimle alakalı port ve protokol katmanıdır. 

5. Oturum Katmanı       : İki taraf arasındaki konuşma anlaşması katmanıdır. 

6. Sunum Katmanı        : Veri biçimi ve şifrelemesi ile alakalı katmandır. 

7. Uygulama Katmanı     : Uygulamalara ait hizmet ve protokol katmanıdır. 

#### OSI KATMANLARI
    
* Network Erişimi   (1-2)   Fiziksel - VeriBağı
* Internet          (3)     AğKatmanı
* Taşıma            (4)     Taşıma
* Uygulama          (5-6-7) Oturum-Sunum-Uygulama

<br>

**Kapsülleme** : Verinin taşımadan önce adres ekleri ve port numaralarıyla iletim için her katman geçimi için hazırlanmasıdır. 

#### ! Uygulamalar arası veri aktarımı sırasında 
* Gönderici Tarafı
    
    * 7 -> 1 kadar katmanlar geçilir. 
    * Data > Segment > Paket > Frame > Bit


* Alıcı Tarafı 

    * 1 -> 7 kadar katmanlar geçilerek katmanlar geçilir. 
    * Bit > Frame > Paket > Segment > Data

## Bu aşamanın notları

- OSI (7): 1 Fiziksel, 2 Veri bağı, 3 Ağ, 4 Taşıma, 5 Oturum, 6 Sunum, 7 Uygulama.
- TCP/IP (4): Uygulama (OSI 5-6-7), Taşıma (4), Internet (3), Network Access (1-2).
- PDU: Data → Segment → Packet → Frame → Bit.
- Kapsülleme: her katman başlık ekler (port, IP, MAC). Alıcıda açma: ters sırada.
- IP uçtan uca sabit, MAC her sıçramada değişir.
- Arıza ararken alttan üste git: kablo → komşular → router → port → uygulama.

## Lab-Raporu

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
