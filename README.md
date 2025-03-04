# Raspberry Pi 

Questa repository contiene i file di configurazione per gestire i container Docker in esecuzione sulla mia Raspberry Pi. Il setup include un reverse proxy con Nginx, Home Assistant per la domotica, e una media stack completa per lo streaming di film e serie tv.

## MediaStack

### 🛡️ VPN Proxy - Gluetun
Gluetun viene utilizzato per instradare il traffico di alcuni container attraverso una VPN.
- Nel mia configurazione solo il container qbittorrent è proxato dietro la VPN
- Utilizzo AirVPN come provider perchè permette il port-forwarding

### 🎬 Radarr - Gestione Film
- Permette di cercare, scaricare e gestire la libreria di film.
- Si integra con qBittorrent per il download e Prowlarr per gestire gli indexers.
- Organizza automaticamente i file scaricati.

### 📺 Sonarr - Gestione Serie TV
- Simile a Radarr, ma per le serie TV.
- Si integra con qBittorrent per il download e Prowlarr per gestire gli indexers.
- Scarica automaticamente nuovi episodi.
- Permette di mantenere organizzata la libreria.

### 📽️ Jellyfin - Media Server
- Server multimediale open-source per la gestione di film, serie TV e musica.
- Streaming locale e remoto.
- Compatibile con dispositivi multipli, inclusi smartphone, smart TV e PC.
- Ha qualche problema di transcodifica sul raspberry. (Consiglio, il container dovrebbe girare su una macchina con una GPU)

### ⬇️ qBittorrent - Client Torrent
- Client torrent con interfaccia web semplice e intuitiva.
- Collegato a Gluetun per mantenere la privacy nella rete torrent.
- Gestione avanzata delle code di download.

### 🔍 Prowlarr - Indicizzatore
- Aggregatore di indexer per Radarr e Sonarr.
- Facilita la ricerca dei contenuti.
- Interfaccia per aggiunta e rimozione di trackers.

### 🛑 FlareSolverr - Bypass CAPTCHA
- Utilizzato per superare i CAPTCHA nei motori di ricerca per torrent.
- Si integra con Prowlarr per bypassare il CAPTCHA di Clouflare.

### 🏠 Homarr - Dashboard di gestione
- Dashboard per monitorare e accedere ai servizi da un'unica interfaccia.
- Integrazione con i container Docker.

## Come Usare

### 1️⃣ Prerequisiti
- **Docker** e **Docker Compose** installati sulla Raspberry Pi.
- **VPN** provider con possibilità di port-forwarding
### 2️⃣ Avvio dello Stack
Esegui il comando seguente nella cartella contenente il file `docker-compose.yml`:
```sh
git clone git@github.com:MaxKappa/raspberry.git
cd mediastack
docker-compose up -d
```

### 3️⃣ Accesso ai Servizi
| Servizio     | URL |
|-------------|---------------------------------|
| Radarr      | http://localhost:7878         |
| Sonarr      | http://localhost:8989         |
| Jellyfin    | http://localhost:8096         |
| qBittorrent | http://localhost:8282         |
| Prowlarr    | http://localhost:9696         |
| Homarr      | http://localhost:7575         |

### Configurazione
- È possibile configurare i vari servizi da web utilizzando la loro documentazione (https://wiki.servarr.com/)
