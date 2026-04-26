# opecka.github.io
# VM WARE vms stroje (NASTAVENÍ)
Virtual Network Editor
- odšktrnout Use Local DHCP service to distribute IP address to VMs

Windows Server 2022 
- novy virtualni stroj
- (typical)
- (I will install the operating system later)
- Microsoft Windows - Windows Server 2022
- location : C:\vms (prostě složka vms)
- Store Virtual disk as a single file
- Edit virtual Machine
- Processors: 1
- Cores per processor: 3-4 (záleží na učebně)
- Memory: 4 GB RAM
- Nasadit .ISO file
- zapnout Machine
- DESKTOP EXPERIENCE verze!!

Linux Mint 
- OS: Linux
- Version: Ubuntu 64-bit
- hardware settings stejně
- Network settings DHCP automatic

Windows 10/11
- OS: Microsoft Windows
- version: Windows 10/11 x64
- hardware settings stejně
- Windows 11/10 Education
- 

# Windows Server 2022 (Settings)
- Domain name změnit !! --> Restart now
- install tools (D:/setup.exe) --> restart now
- Změnit Network Adapter parametry IPv4
- Podivat se do VMWare app a tam Edit > Virtual network editor
- Zjistit Subnet IP, Subnet mask (zustava stejně 255.255.255.0), Gateway IP
- do Serveru nastavit IP adresu, Subnet Mask, Default Gateway, Preferred DNS Server (stejně jako gateway)

DHCP Server
- add roles DHCP Server
- dokončit nastavení
- nastavit Scope (rozsah)
- nastavit reservations pro Linux a Windows (MAC adresy - jenom čisla a pismena)
- Scope options přidat 003 Router (gateway IP) a 006 DNS Servers (Ip adresa školní)

DNS Server
- add roles DNS Server
- DNS manager
- configure DNS server
- název domény např server22.com
- nastavit IP adresu --> adresa windows serveru
- do DHCP manager > Scope "název" > Scope options
- přidat DNS adresu do "006 DNS Servers" (primární=adresa serveru, alternativní=školní/1.1.1.1)
- vypnout a zapnout síť na linuxu a windows 11/10 a ověřit zda je všechno správně (např. prohlížeče)



  
- 

