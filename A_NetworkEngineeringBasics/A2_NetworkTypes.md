## Ağ Ölçüleri
* Bandwidth : Bağlantının teoride taşıyabileceği maksimum miktardır. 
* Latency : Verinin hedefe olan erişim süresini ifade etmek için kullanılır. 
* Throughpart : Anlık olarak gerçekleşen veri hızı ve erişim süresidir. 

Ağ Türleri
* PAN     : Personal Area Network -> Telefon kulaklık vb gibi yakın mesafe ağlardır.      
* LAN     : Local Area Network -> Ev ofis gibi bölgesel ağlardır. 
* WLAN : Wireless Local Area Network -> Kablosuz olarak kurulan bölgesel ağlardır. 
* MAN    : Metropolitan Area Network -> Şehir geneli kurulan ağdır. Belediye veya operatör gibi.
* WAN.   : Wide Area Network -> Dünya geneli kurulan ağlardır. 
* SAN     : Storage Area Network -> Sunucuları, disklere bağlayan disk trafiği ağlarıdır. 
* VPN     : Virtual Private Network -> Genel ağ üzerinde kurulan, şifreli tünel ağdır. 
* CLOUD: İnternet üzerinden kiralanan ağ ve hizmet sistemleridir. 

Ağ Tipleri
* Client - Server -> Merkezi sunucu vardır. Yönetilmesi kolaydır. Mail / Web server. 
* Peer to peer -> Merkezi sunucu yoktur. Yönetilmesi zordur. Torrent sistemleri. 

// Internetin Çalışması 
Ağ -> ISP -> Bölgesel Omurga ağlar -> Değişim noktaları(IXP) -> Veri Merkezi (Sunucu)

## Bu aşamanın notları
- **Bandwidth** = kapasite (Mbps), **latency** = gecikme (ms), **throughput** = gerçekte akan hız.
- **1 byte = 8 bit**; 100 Mbps ≈ 12,5 MB/s.
- Küçük işlerde latency, büyük dosyalarda bandwidth belirleyicidir.
- **PAN** kişisel, **LAN** bina, **WLAN** kablosuz LAN, **MAN** şehir, **WAN** uzak mesafe, **SAN** depolama ağı, **VPN** şifreli tünel, **Cloud** başkasının veri merkezindeki kaynaklar.
- İnternet = birbirine bağlı ağlar. **Client-server**: merkezi sunucu. **P2P**: herkes hem alıcı hem verici.

## Lab-Raporu
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