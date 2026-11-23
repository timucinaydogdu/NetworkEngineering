# Ağ temelleri
* Client : Bir hizmeti isteyen cihaz yada programdır. 
* Server : İstek bekleyen ve cevap veren cihaz yada proğramdır. 
* Host : Ağ üzerinden IP alabilen tüm cihazlardır. 
* IP Adresi : Cihazın ağ üzerindeki adresidir. 
* Mac Adresi : Ağ kartı üzerindeki verilen adrestir. 
* Port : Aynı cihazda çalışan hizmetler için erişim kapı numarasıdır. 
* Soket : IP adresi ve port numarasının tam yoludur. 
* Protokol : Cihazların birbirleriyle iletişim kurma kurallarıdır. 
* Paket : Veri paketlerinin Router sonrakindaki veri parçalarına bölünmesidir. 
* Frame : Veri paketlerinin Ağ üzerindeki taşınma sırasındaki paket halidir. 

www.xx.com > Dns Dönüşümü > Protokol Seçimi > Veri Framelere ayrılır > Routera iletilir > Hedef sokette iletilir > Siteden cevap verir. 

## Bu aşamanın notları
- **Client** ister, **server** verir. Aynı cihaz ikisi de olabilir.
- **Host** = ağdaki IP adresi olan her cihaz.
- **IP** mantıksal adres, **MAC** fiziksel adres, **port** programın kapısı.
- **Socket** = IP + port (`192.168.1.20:443`).
- **Protokol** = ortak kurallar. **Paket** IP katmanının, **frame** yerel ağ katmanının veri birimi.
- Yerel ağda MAC "bir sonraki komşu"yu, IP "son hedefi" gösterir.

## Lab-Raporu
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