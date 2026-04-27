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
- sudo apt install open-vm-tools-desktop

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

ADDS
- add roles ADDS
- add new forest 
- doplnit název
- nastavit heslo při prihlášení do domény
- po instalaci je hned RESTART
- DHCP manager autorizace, aby fungovalo Scope
- do síťového adapteru na Windows Serveru změnit DNS adresy (primární=adresa dns, alternativní=školní/1.1.1.1)
- ADUC (Active Directory Users and Computers)
- nahoře tools > ADUC
- pravým klikneme na naše doméno
- new > organizational unit > přidat název
- přidat Usera
- GPM (Group Policy Management)
- Domains > náš server > náš organizational unit
- přidat GPO (Grou Policy Object)
- pravým Edit
- v User configuration si můžeme vypnout/zapnout prává uživatele na stroji
- DNS manager
- Forward lookup Zones > náš servername > Properties
- nastavit Type na Active Diretory (Change > zašktrnout Store the zone ... atd)
- powershell zadat ipconfig /registerdns, net stop netlogon, net start netlogon
- V DNS manager REFRESH
- TED DO WINDOWS 11/10
- Systém > Doména nebo pracovní skupina > změnit > je členem domény > napsat naší doménu
- Zadat uživatelské jméno a heslo, které jsme si založili uživatele v organizational unit
- restartovat nyní
- přilhásit se > Others > zadat uživatelské jméno a heslo
- Jelikož jsme si přidali nějaké práva např. zákaz přidavání tiskárny
- vyzkoušíme jestli se nám podaří přidat tiskárnu
- Pokud nejde --> správně

Web Server IIS
- add roles Web Server IIS
- přidat FTP server
- IIS manager
- vyzkoušet jestli funguje web server (locahost na serveru, windows11/10: "adresa serveru:80")
- přidat FTP site
- nastavit jméno a cestu složky
- necháme All Unassigned a port 21
- No SSL
- Authentication > Basic
- Authorization > All users
- Permissions: READ, WRITE
- REFRESH sites
- na windows 11/10 WinSCP připojit se k ftp
- vytvořit soubor pro test
- na Linux Mint instalovat filezilla

SSH server a klient
Linux Mint
- nainstalovat ssh
- nainstalovat Remmina
Windows 11/10
- pokud se chceme z linuxu připojit k uživateli, který je přiřazen k doméně musíme přidat uživatel do vzdálené plochy
- Windows Ikon > System > vzdálená plocha > uživatelé vzdálené plochy > přidat uživatele
- zapnout ssh service na windowsu 11 (přikazy si můzeme vygenerovat pomocí AI)
Windows Server 22
- ověření ssh jestli funguje (přikazy si můzeme vygenerovat pomocí AI)
- zkusíme si připojit WS22 --> L, L-->WS22, Win10 --> L, L --> Win10

Web Server Windows Apache Xampp
- instalace Xampp
- DocumentRoot: C:/xampp/htdocs
- přidavaní Virtual host: C:/xampp/apache/conf/extra/httpd-vhosts.conf
- přidavání hostname: C:/Windows/System32/drivers/etc/hosts
Linux Mint Apache
- sudo apt install apache2
- sudo systemctl enable apache2
- sudo systemctl start apache2
- sudo systemctl status apache2
- přidavání webu /etc/apache2/sites-available/
- zkopírovat 000-default.conf (přejmenovat a upravit podle svého)
- DocumentRoot /var/www/html
- ServerName "název"
- ServerAdmin "webmaster@název"
- /etc/hosts (jako root) přidat 127.0.0.1 + název
- sudo a2ensite název.conf
- sudo systemctl reload apache2
- test stránky
- Windows --> Linux, přidat do C:/Windows/System32/drivers/etc/hosts adresu stroje a název stránky
- Linux --> Windows, přidat do /etc/hosts (root) přidat adresu stroje a název stránky
- 
