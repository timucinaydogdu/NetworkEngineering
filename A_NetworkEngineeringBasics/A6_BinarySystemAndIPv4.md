## İkili sistem ve IPv4
* **Binary(İkiliSistem)** : Matematiksel iki taban sistemidir. 10 luk ve 16 lık tabanlar için taban dönüşümleri yapılır. 

    * 128 64 32 16 8 4 2 1 Dizesi hesaplama kolaylığı sağlar. 

* **IPv4** : Bir IP adresi 4 adet(OKTET) 4 bit(0-255) sayıdan alışan ikili sayı bütünüdür. 

* **SubnetMask**        : Kullanıcı sayı limitini belirten ağ belirticisidir. 

* **Network**           : IP'sinin ağ adresini belirten kısımdır. 

* **Host**              : IP adresinin kullanıcı cihaz sayısının belirlendiği kısımdır. 

* **CIDR Gösterimi**    : IP adresinin ve SubnetMaskın basit şekilde gösterilmesidir. 

    * 192.168.0.1/24 -> 255.255.255.0 - 24 bit'i subnetmasktır. 

// 192.168.0.1       -> 4 Oktet, 32 Bittir.<br>
// 192.168.0.1/24    -> Alt ağmaskesi 24 bittir. 

## Adres Tiplerinin Kullanım Alanları
* İç ağ adresleri, internete yönlendirilmez. 
    * 10.0.0.0/8
    * 172.16.0.0/12
    * 192.168.0.0/16

* Cihazın yazılımsal IP adresidir. Loopback için kullanlır. 
    * 127.0.0.1

* DHCP'den adres alınmadığında local olarak alınan adres. 
    * 169.254.0.0/16

* Operatörlerin kullandığı paylaşımlı IP'lerdir. 
    * 100.64.0.0/10

* Multicast yayın IP'leridir. 
    * 224.0.0.0
    * 239.255.255.255

* **IP Büyüklükleri**
    * A/	1 – 126	/8 · 255.0.0.0	Çok büyük ağlar 
    * B/	128 – 191	/16 · 255.255.0.0	Orta büyüklük
    * C/	192 – 223	/24 · 255.255.255.0	Küçük ağlar (ev, ofis)
    * D/	224 – 239	-	Multicast
    * E/	240 – 255	-	Deneysel/ayrılmış

## Bu aşamanın notları
* Bit = 0 veya 1. 8 bit = 1 oktet. Değerler: 128, 64, 32, 16, 8, 4, 2, 1. En büyük oktet değeri 255.
* IPv4 adres = 32 bit = 4 oktet, ondalık ve noktalı yazılır.
* Subnet mask: 1'ler ağ, 0'lar host. /24 = 255.255.255.0 = 24 tane 1.
* Kullanılabilir host sayısı = 2h − 2 (h: host bit sayısı).
* Özel: 10/8, 172.16–31/12, 192.168/16. Loopback: 127.0.0.1. APIPA: 169.254.x.x. CGNAT: 100.64/10.
* Hex mask okuma: ff = 255, 00 = 0 (0xffffff00 = /24).

## Lab-Raporu
- Bilgisayarın ip ve subnetMaskı
    - netmask 16 lık sistemde gelir. FF-> 255 e karşılık gelir. 
```bash
ifconfig en0 | grep "inet "
ipconfig getifaddr en0
ipconfig getoption en0 subnet_mask
```
```bash
inet 192.168.1.178 netmask 0xffffff00 broadcast 192.168.1.255
192.168.1.178
255.255.255.0
```
---
---

- Terminalde ikilik dönüşümü 
```bash
echo "obase=2; 192" | bc
echo "obase=2; 168" | bc
echo "ibase=2; 11000000" | bc
```
```bash
11000000
10101000
192
```
---
---
-  Özel ve genel IP farkı
```bash
ipconfig getifaddr en0
curl -s https://api.ipify.org; echo
```
```bash
192.168.1.20
198.51.100.7
```
---
---