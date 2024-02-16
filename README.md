## Portfolio IT / Administration Systèmes et Réseaux

### Inventaire du matériel (hors IoT, smartphones et câbles RJ45)
|Nom	|Type de matériel	|
|---	|---	|
|Internet Box	|Routeur	|
|Router	|Routeur	|
|PC1	|PC	|
|PC2	|PC	|
|Server	|PC	|
|Laptop1	|Ordinateur Portable	|
|Switch1	|Commutateur	|

### Schéma du réseau
<img src="./Images/HomeLab_IT.png" width=800>

### Configuration des routeurs
#### Internet Box
Serveur DHCP: 172.21.42.1/16 à 172.21.42.254/16  
DNS: 8.8.8.8, 1.1.1.1  
Wifi: SSID masqué, WPA2  
Wifi invité désactivé  
Réponse ping désactivée  
Contrôle par adresse MAC désactivé  

#### Router
Serveur DHCP: 172.22.73.10/16 à 172.22.73.90/16  
DNS: 172.22.73.110, 172.22.73.130  
Wifi: SSID visible, WPA3  
Wifi invité désactivé  
Réponse ping désactivée  
Contrôle par adresse MAC activé  
Routage statique: 172.21.0.0/16 via 172.21.122.254

### Subnet 1
| Nom          | Rôle   | OS     | Adressage | IP                | Gateway        |
|--------------|---------|--------|-----------|-------------------|----------------|
| Internet Box | Gateway | Linux  | Manuel    | 172.21.122.254/16 | 127.0.0.1      |
| IoT          | *       | *      | DHCP      | *                 | 172.21.122.254 |
| Router       | *       | Client | Manuel    | 172.21.122.1/16   | 172.21.122.254 |

### Subnet 2
| Nom     | Rôle                  | OS                  | Adressage | IP                 | Gateway      |
|---------|------------------------|---------------------|-----------|--------------------|--------------|
| Router  | Gateway                | *                   | Manuel    | 172.22.122.1/16    | 127.0.0.1    |
| PC1     | Client                 | Windows 10          | DHCP      | 172.22.73.50/16    | 172.22.122.1 |
| PC2     | Client                 | Windows 10          | DHCP      | 172.22.73.60/16    | 172.22.122.1 |
| Laptop1 | Client                 | Ubuntu              | DHCP      | 172.22.73.70/16    | 172.22.122.1 |
| Server  | Hyperviseur            | Proxmox 7           | Manuel    | 172.22.73.100/16   | 172.22.122.1 |
| SRV1    | DNS + Active Directory | Windows Server 2019 | Manuel    | 172.22.73.110/16   | 172.22.122.1 |
| SRV2    | NAS                    | TrueNAS             | Manuel    | 172.22.73.120/16   | 172.22.122.1 |
| SRV3    | Serveur Docker + DNS   | Ubuntu              | Manuel    | 172.22.73.130/16   | 172.22.122.1 |
| SRV4    | SIEM                   | Wazuh               | Manuel    | 172.22.73.140/16   | 172.22.122.1 |
| SRV5    | IDS                    | Suricata            | Manuel    | 172.22.73.150/16   | 172.22.122.1 |
| C1      | DNS                    | AdGuard             | Manuel    | 172.22.73.130:53   | 172.22.122.1 |
| C2      | IoT server             | Home Assistant      | Manuel    | 172.22.73.130:8000 | 172.22.122.1 |
| C3      | Media Center           | Jellyfin            | Manuel    | 172.22.73.130:9000 | 172.22.122.1 |
