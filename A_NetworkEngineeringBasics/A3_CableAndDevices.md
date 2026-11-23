## Kablolar Ve Cihazlar
* Bakır -> Verinin bakır tablo üzerinde taşınmasıdır. Hızlı ve kolay kurulur. 
	* CAT5e : 1 Gbps / 100m -> Ofis ev tipi kullanımı vardır. 
	* CAT6   : 1 Gbps / 100m & 10 Gbps / 55m -> Ofis veri merkezi. Kısa mesafe.
	* CAT6a : 10 Gbps / 100m -> Veri merkezi
	* DAC (Bakır Twinax) : 10 Gbps / 3m  -> Sunucu kabin içi kullanımı var. 
	* Multi Mode Fiber : 10 Gbps / 300m & 100Gbps / 100m -> Bina içi, veri merkezinde 
	* Single Mode Fiber : 40-100 Gbps / 20km -> Binalar arası ve şehirler arası kullanım. 
* Fiber -> Verilerin fibercam üzerinden ışıkla taşınmasıdır. Pahalı ve kırılgandır. 
* Kablosuz -> Kurulumda kablo gerektirmeyen sistemlerdir. Sinyal ortamı paylaşılır. 

Ağ Tipleri
* HUB -> Gelen veriyi, sahip olduğu portlara direk kopyalar. Kontrol edilmez. 
* SWITCH -> Ağ cihazlarını adreslerine bağlar. Sadece doğru porta iletilir. MAC adresine bakar. 
* ROUTER -> Farklı ağları birbirine bağlar. IP üzerinde iletişime geçer. 
* MODEM -> ISP gelen sinyali, ağ sinyaline çevirerek iletişimi sağlar. 
* ACCESS POINT -> Kablosuz ağ sinyallerini, kablolu ağlara köprüleme yapmayı sağlar. 

### Switch'in MAC öğrenmesi süreci<br>
Switch A -> B sinyal -> (Tablo boş. Tüm portrala flood) -> Switch A nın MAC Adresini öğrenir. <br>
Switch B -> A sinyal -> (Sinyal direk A'ya gider.) -> Switch B nın MAC Adresini öğrenir. 

## Bu aşamanın notları
- **Bakır (UTP)**: ucuz, en fazla 100 m.<br> 
**Fiber**: hızlı, uzun mesafe, parazitsiz;<br> 
**single-mode** kilometreler,<br> 
**multi-mode** yüzlerce metre.<br> 
**Kablosuz**: esnek ama paylaşımlı.
- Rack içi çok kısa hatlar için **DAC**,<br> 
binalar arası için **single-mode fiber**.
- **Hub** herkese kopyalar,<br>
 **switch** MAC'e bakıp doğru porta gönderir (MAC tablosunu öğrenir).
- **Router** IP'ye bakıp farklı ağları bağlar;<br>
 **modem** operatör sinyalini çevirir;<br>
  **AP** kablosuzu kabloluya bağlar.
- Ev kutusu = modem/ONT + router + switch + AP bir arada.

## Lab-Raporu
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