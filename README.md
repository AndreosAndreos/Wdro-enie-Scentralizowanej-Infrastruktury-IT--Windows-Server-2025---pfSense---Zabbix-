# Wdrożenie Scentralizowanej Infrastruktury IT (Windows Server 2025 & pfSense & Zabbix)

## 📌 O projekcie
Kompleksowe wdrożenie scentralizowanego środowiska IT dla przedsiębiorstwa, zrealizowane jako projekt inżynierski na Państwowej Akademii Nauk Stosowanych w Nysie. System integruje nowoczesne usługi katalogowe Microsoft z otwartoźródłowymi rozwiązaniami z zakresu cyberbezpieczeństwa oraz monitoringu.

## 🏗️ Architektura i technologie
Sercem projektu jest hiperwizor **Proxmox VE**, na którym uruchomiono odizolowane segmenty sieci w celu zapewnienia maksymalnego bezpieczeństwa.

* **Wirtualizacja:** Proxmox VE (Bare-metal).
* **Usługi Katalogowe:** Windows Server 2025 Datacenter w konfiguracji **High Availability** (Główny oraz dodatkowy kontroler domeny z pełną replikacją AD/DNS/DHCP).
* **Sieć i Bezpieczeństwo:** pfSense 2.7.2, system IDS/IPS Suricata, VPN (Tailscale oraz OpenVPN).
* **Dostęp zdalny i Uwierzytelnianie:** Uruchomienie bezpiecznych tuneli VPN (OpenVPN) zintegrowanych z usługą **RADIUS (rola NPAS)** na Windows Server 2025. Pozwala to na centralne zarządzanie uprawnieniami dostępu zdalnego bezpośrednio z kont w Active Directory.
* **Usługi Webowe:** Serwer **IIS (Internet Information Services)** wdrożony w strefie DMZ do hostowania zasobów wewnętrznych.
* **Monitoring:** Zabbix 7.4 (SNMP & Agenci) zainstalowany na systemie Ubuntu Server 22.04.

## 🌐 Projekt sieci
Infrastruktura została podzielona na logiczne strefy bezpieczeństwa zarządzane przez firewall pfSense:
* **WAN:** Dostęp zewnętrzny z wykorzystaniem dynamicznego DNS (DuckDNS).
* **DMZ (192.168.40.0/24):** Strefa zdemilitaryzowana dla serwerów Windows Server 2025.
* **LAN (192.168.50.0/24):** Sieć lokalna dla stacji roboczych Windows 11 pracujących w domenie.
* **Monitoring (192.168.60.0/24):** Wydzielona sieć przeznaczona dla serwera monitorującego Zabbix.

## 📸 Wizualizacja i Galeria

### ☁️ Środowisko Wirtualizacji
* [Widok węzła Proxmox VE z listą maszyn wirtualnych](img/Proxmox_infrastruktora.png)
  * *Opis: Zarządzanie zasobami obliczeniowymi w oparciu o hiperwizor Proxmox VE. Widoczna separacja ról serwerowych oraz maszyn klienckich Windows 11.*

### 🌐 Architektura Sieci i AD
* [Topologia sieci (Schemat logiczny)](img/Topologia.png)
* [Struktura Jednostek Organizacyjnych w Active Directory](img/Struktura%20organizacji.png)

### 🔧 Konfiguracja Systemowa i Bezpieczeństwo
* [Aktywne role serwerowe (AD DS, DHCP, DNS, IIS, NPAS)](img/MainServer.png)
* [Wykaz wdrożonych obiektów zasad grupy (GPO)](img/GPO.png)
* [Konfiguracja reguł Firewall dla segmentu DMZ w pfSense](img/DMZrules.png)
  * *Opis: Dokumentacja konfiguracji ról, polityk bezpieczeństwa (np. blokada USB) oraz segmentacji ruchu.*

### 🖥️ Monitoring i Operacje
* [Mapa logiczna infrastruktury w systemie Zabbix 7.4](img/Mapa%20logiczna%20-%20zabbix.png)

## 🛡️ Kluczowe funkcjonalności
* **Wysoka dostępność (HA):** Mechanizm replikacji bazy AD oraz failover usług DHCP/DNS pomiędzy dwoma kontrolerami domeny.
* **Active Directory:** Pełna struktura OU, zarządzanie grupami oraz zaawansowane polityki GPO (hardening systemów, mapowanie zasobów).
* **Ochrona sieci:** Implementacja systemu IDS/IPS Suricata oraz precyzyjne filtrowanie ruchu wychodzącego (Egress Filtering) w strefie DMZ.
* **Remote Access:** Bezpieczne tunele VPN oparte na protokołach WireGuard (Tailscale) oraz SSL/TLS (OpenVPN) z autoryzacją RADIUS.
* **Observability:** Centralny monitoring Zabbix śledzący wydajność maszyn oraz dostępność krytycznych usług systemowych.

## 📁 Dokumentacja
Pełna dokumentacja techniczna projektu w formacie PDF znajduje się w folderze `/doc`.
