## Protokoller, Portlar ve APR
* **Protokol** : İletişime geçen ve geçilen programlar arası ortak iletişim kurallarıdır.

* **Port** : Protokolle bağlı iletişime geçilen program veya hizmetlerin erişim noktasıdır. 
	* Web Erişimi: 
        * 80 -> HTTP Web erişim portu (Şifresiz)
		* 443 -> HTTPS Güvenli web erişim portu (Şifreli)

	* Uzaktan Erişim :
        * 22 -> SSH Erişim  portu (Şifreli)
		* 23 -> TELNET Erişim  portu (Şifresiz)
		* 3389 -> RDP (RemoteDesktop) Erişim portu (Şifreli)

	* Dosya Erişimi :
        * 20 / 21 -> FTP Erişim portu (Şifresiz)
		* 22 -> SFTP Erişim portu (Şifreli)

	* Eposta Erişimi : 
        * 25 / 587 -> SMTP Erişim portu (Şifreli)
		* 143 / 993 -> IMAP Erişim portu (Şifreli)
		* 110 / 995 -> POP3 Erişim portu (Şifreli)

	* Ağ Erişimi : 
        * 53 -> DNS Erişim portu (Şifresiz)
		* 67 / 68 ->DHCP Erişim portu (Şifresiz)
		* 123 -> NTP Erişim portu (Şifresiz)
		* 161 / 162 -> SNMP Erişim portu (Şifreli)
		* 514 -> SYSLOG Erişim portu (Şifresiz)
		* Numarasız -> ICMP Erişim portu (Şifresiz)

* Veri Taşıma Tipleri 
	*  TCP/IP -> Veri erişimi karşılıklı onaylanır. Yavaş ama güvenlidir.
	* UDP -> Veri gönderilir ama onay beklenmez. Hızlı ama veri kaybı ihtimali vardır. 

## Bu aşamanın notları
- **Portlar:** SSH 22, HTTP 80, HTTPS 443, DNS 53, SMTP 25, DHCP 67/68, NTP 123, SNMP 161, RDP 3389.
- **Şifreli:** SSH, HTTPS, SFTP, IMAPS. **Şifresiz (kaçın):** Telnet, HTTP, FTP, POP3 düz.
- **TCP** güvenilir ve onaylı (web, SSH, e-posta). **UDP** hızlı ve garantisiz (DNS, DHCP, ses/video).
- TCP bağlantı öncesi **3 adımlı el sıkışma** yapar (SYN, SYN-ACK, ACK).
- **ARP**: yerel ağda IP'den MAC bulur. Soru herkese (broadcast), cevap sadece sorana. Sonuç ARP tablosunda saklanır.
- İnternete giderken ARP ile **router'ın** MAC'i sorulur.

## Lab-Raporu
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
