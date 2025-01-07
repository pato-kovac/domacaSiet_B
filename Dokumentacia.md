# Domáca sieť B

## Čo som zakomponoval:
* 1 "Hlavný" Router-PT
* 4 Wireless Routre typu WRT300N <sub>(vybral som tento typ routera, pretože má zabudovaný AP, vysiela wi-fi signál a ma jednoduchšie rozhranie ako iné bezdrátové routre)</sub>
* 1 Switch-PT
* 2 PC-PT <sub>(jeden pre otca, druhý pre hosťa)</sub>
* 3 Laptop-PT  <sub>(mama, ferko a jožko)</sub>
* 4 servery <sub>(smarthome, DNS, 2 webové stránky)</sub>
* 1 smarthome kamera <sub>(IoT1)</sub>

## Postupovaie pri práci
1. Premenoval som si všetky zariadenia, aby som mal lepší prehľad
2. Vypol som Router-PT a odstránil som nepotrebné moduly (porty) PT-ROUTER-NM-1FFE a PT-ROUTER-NM-1S
3. Následne som pridal ďalšie 3 moduly PT-ROUTER-NM-1CFE pre zvýsenie kapacity a potom som router opäť zapol
4. Zostavil som si zariadenia do stromovej topológie (tree) a následne som ich prepojil automatickým prepojením:
    * a. Router-PT:
         * PORT: Fa0/0 -> PORT: 0/1, Router RODIČIA
         * PORT: Fa1/0 -> PORT: 0/1, Router HOSTIA
         * PORT: Fa2/0 -> PORT: 0/1, Router DETI
         * PORT: Fa3/0 -> PORT: 0/1, Router SMARTHOME
         * PORT: Fa4/0 -> PORT: Fa0/1, Switch-PT
    * b. Switch-PT:
         * PORT: Fa1/1 -> PORT: Fa0, DNS server
         * PORT: Fa2/1 -> PORT: Fa0, web server - YT Kids
         * PORT: Fa3/1 -> PORT: Fa0, web server - Nevhodná stránka
5. Všetky ostatné zariadenia, ktoré budú pripojené k Wireless-Routrom som vypol a pridal (nahradil) som k nim wi-fi sieťovú kartu WPC300N, po inštalácii som zariadenia zapol <sub>(PC OTEC, Laptop MAMA, PC HOSŤ, Laptop FERKO, Laptop JOŽKO, Server SMARTHOME, Smarthome Kamera)</sub>
6. Skontrolovať, či sú všetky porty na Routri-PT zapnuté

### Konfigurácia routerov
1. **Router-PT**
    * IP konfigurácia portov:
        * Fa0/0: IPv4 192.168.10.1, Maska 255.255.255.0 <sub>RODIČIA</sub>
        * Fa1/0: IPv4 192.168.20.1, Maska 255.255.255.0 <sub>HOSTIA</sub>
        * Fa2/0: IPv4 192.168.30.1, Maska 255.255.255.0 <sub>DETI</sub>
        * Fa3/0: IPv4 192.168.40.1, Maska 255.255.255.0 <sub>SMARTHOME</sub>
        * Fa4/0: IPv4 192.168.50.1, Maska 255.255.255.0 <sub>WEB</sub>
2. **Router RODIČIA**
      * Internet:
        * IP configuration = static
        * IPv4: 192.168.1.1
        * Subnet Mask: 255.255.255.0
        * Default Gateway: 192.168.1.1
        * DNS Server: 192.168.50.10
      * LAN:
        * IPv4: 192.168.20.1
        * Subnet Mask: 255.255.255.0
      * Wireless:
        * SSID = "Rodicia"
        * Authentication = WPA2-PSK <sub>pre väčšie zabezpečenie</sub>
        * PSK Pass Phrase = "Rodicia123"
        * Encryption type = AES
3. **Router HOSTIA**
      * Internet:
        * IP configuration = static
        * IPv4: 192.168.1.2
        * Subnet Mask: 255.255.255.0
        * Default Gateway: 192.168.1.1
        * DNS Server: 192.168.50.10
      * LAN:
        * IPv4: 192.168.10.1
        * Subnet Mask: 255.255.255.0
      * Wireless:
        * SSID = "Hostia"
        * Authentication = WPA2-PSK
        * PSK Pass Phrase = "Hostia123"
        * Encryption type = AES
4. **Router DETI**
      * Internet:
        * IP configuration = static
        * IPv4: 192.168.1.3
        * Subnet Mask: 255.255.255.0
        * Default Gateway: 192.168.1.1
        * DNS Server: 192.168.50.10
      * LAN:
        * IPv4: 192.168.30.1
        * Subnet Mask: 255.255.255.0
      * Wireless:
        * SSID = "Deti"
        * Authentication = WPA2-PSK
        * PSK Pass Phrase = "Deticky123" <sub>"Deti123" je príliš krátke heslo</sub>
        * Encryption type = AES
5. **Router SMARTHOME**
      * Internet:
        * IP configuration = static
        * IPv4: 192.168.1.4
        * Subnet Mask: 255.255.255.0
        * Default Gateway: 192.168.1.1
        * DNS Server: 192.168.50.10
      * LAN:
        * IPv4: 192.168.40.1
        * Subnet Mask: 255.255.255.0
      * Wireless:
        * SSID = "Smarthome"
        * Authentication = WPA2-PSK
        * PSK Pass Phrase = "Smarthome123"
        * Encryption type = AES

### Konfigurácia zariadení
Zariadenie > Desktop > Ip Configuration
1. **PC OTEC**
    * IP Configuration = static
    * IPv4: 192.168.10.10
    * Subnet Mask: 255.255.0.0
    * Default Gateway: 192.168.10.1
    * DNS Server: 192.168.50.10
2. **Laptop MAMA**
    * IP Configuration = static
    * IPv4: 192.168.10.20
    * Subnet Mask: 255.255.0.0
    * Default Gateway: 192.168.10.1
    * DNS Server: 192.168.50.10
4. **PC HOSŤ**
    * IP Configuration = static
    * IPv4: 192.168.20.10
    * Subnet Mask: 255.255.0.0
    * Default Gateway: 192.168.20.1
    * DNS Server: 192.168.50.10
5. **Laptop FERKO**
    * IP Configuration = static
    * IPv4: 192.168.30.10
    * Subnet Mask: 255.255.0.0
    * Default Gateway: 192.168.30.1
    * DNS Server: 192.168.50.10
6. **Laptop JOŽKO**
    * IP Configuration = static
    * IPv4: 192.168.30.20
    * Subnet Mask: 255.255.0.0
    * Default Gateway: 192.168.30.1
    * DNS Server: 192.168.50.10
6. **Server SMARTHOME**
    * IP Configuration = static
    * IPv4: 192.168.40.10
    * Subnet Mask: 255.255.0.0
    * Default Gateway: 192.168.40.1
    * DNS Server: 192.168.50.10
6. **Smarthome Kamera**
    * Settings:
      * Gateway/DNS IPv4 = static
      * Default Gateway: 192.168.40.1
      * DNS Server: 192.168.50.10
    * Wireless0:
      * IP Configuration = static
      * IPv4: 192.168.40.20
      * Subnet Mask: 255.255.0.0

### Konfigurácia webovej časti siete
1. **Switch-PT**
    * Zapnúť 3 PT-ROUTER-NM-1CFE porty
2. **DNS server**
DNS server > Desktop > Ip Configuration
    * IP Configuration = static
    * IPv4: 192.168.50.10
    * Subnet Mask: 255.255.255.0
    * Default Gateway: 192.168.50.1
    * DNS Server: 192.168.50.10
DNS server > Services > DNS
    * DNS Service = ON
    * Pridať 2x:
        * Name1: nevhodnastranka.com
        * Name2: youtubekids.com
        * Tpye1: A Record
        * Type2: A Record
        * Address1: 192.168.50.30
        * Address2: 192.168.50.20
3. **Server Youtube Kids**
YT Kids server > Desktop > Ip Configuration
    * IP Configuration = static
    * IPv4: 192.168.50.20
    * Subnet Mask: 255.255.255.0
    * Default Gateway: 192.168.50.1
    * DNS Server: 192.168.50.10
YT Kids server > Services > HTTP
    * Zmeniť text headeri v index.html, aby sa dalo rozornať, na ktorej stránke sme
4. **Server Nevhodná stránka**
Server Nevhodná stránka > Desktop > Ip Configuration
    * IP Configuration = static
    * IPv4: 192.168.50.30
    * Subnet Mask: 255.255.255.0
    * Default Gateway: 192.168.50.1
    * DNS Server: 192.168.50.10
Server Nevhodná stránka > Services > HTTP
    * Zmeniť text headeri v index.html, aby sa dalo rozornať, na ktorej stránke sme
  

### Pripojenie zariadení k wi-fi sieti
  * Zariadenie > Desktop > PC Wireless > Connect > Refresh > Vybrať sieť > Zadať heslo
  * <sub>Rodicia = Rodicia123, Hostia = Hostia123, Deti = Deticky123, Smarthome = Smarthome123</sub>
  * <sub>Ak zariadenie nemá desktop rozhranie, tak treba manuálne zadať údaje ako je SSID a Pass Phrase v konfigurácii Wireless0</sub>

### Nastavenie manuálnej konfigurácie siete smarthome
  * Router SMARTHOME > GUI > Wireless > SSID Broadcast = Disabled
  * <sub>V "aplikácii" PC Wireless bude sieť neviditeľná</sub>

### Nastavenie siete Hostia aby mala prístup len na internet, nie do lokálnych sietí
  * Router-PT > CLI
    
        Router> enable
        Router# configure terminal
        Router(config)# access-list 101 deny ip 192.168.20.0 0.0.0.255 192.168.30.0 0.0.0.255         (Blokovanie prístupu medzi sieťami hostí a detí)
        Router(config)# access-list 101 deny ip 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255         (Blokovanie prístupu medzi sieťami hostí a rodičov)
        Router(config)# access-list 101 deny ip 192.168.20.0 0.0.0.255 192.168.40.0 0.0.0.255         (Blokovanie prístupu medzi sieťami hostí a smart home)
        Router(config)# access-list 101 permit ip 192.168.20.0 0.0.0.255 any                          (Povolenie prístupu hostí do internetu)
        Router(config)# interface FastEthernet1/0                                                     (Port hostí)
        Router(config-if)# ip access-group 101 in                                                     (Aplikovanie AC listu)

### Komplikácie
  * Whitelist stránok pre sieť DETI sa mi nepodarilo zrealizovať, wi-fi routre, ktoré som použil, majú GUI rozhranie, ale nemajú CLI. V GUI rozhraní chýba veľa nastavení, nie je tam URL whitelist ale len     blacklist, ktorý som taktiež nevedel spojazdniť. (Napriek príkazu blokovať URL stránky, je nevhodná stránka pre sieť DETI stále dostupná) 
  * S programom sa mi pracovalo celkom ťažko a zadanie mi trvalo splniť omnoho viac času, ako som si predstavoval
