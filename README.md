# librechat-rpi4

# Guida all'installazione di LibreChat

## Passo 1: Rimuovere i container e i volumi esistenti
Rimuovi eventuali container e volumi associati a LibreChat, inclusa la cartella `LibreChat`. Mantieni solo le immagini Docker.

---

## Passo 2: Installare i requisiti
Assicurati di avere i seguenti pacchetti installati:

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common gnupg lsb-release git nodejs npm
```

---

## Passo 3: Clonare il repository
Clona il repository di LibreChat e accedi alla cartella del progetto:

```bash
git clone https://github.com/danny-avila/LibreChat.git
cd LibreChat/
```

---

## Passo 4: Creare il file di configurazione
Apri il file `librechat.yaml` per configurare le variabili ambiente. Usa il comando:

```bash
nano librechat.yaml
```

Incolla il seguente contenuto:

```yaml
# For more information, see the Configuration Guide:
# https://docs.librechat.ai/install/configuration/custom_config.html

# Configuration version (required)
version: 1.0.5
# This setting caches the config file for faster loading across app lifecycle
cache: true
```

Salva con **CTRL+O** e chiudi con **CTRL+X**.

---

## Passo 5: Creare il file `.env`
Copia il file di esempio `.env`:

```bash
cp .env.example .env
```

---

## Passo 6: Scaricare la versione modificata di MongoDB
Scarica l'immagine Docker modificata per MongoDB:

```bash
wget https://github.com/themattman/mongodb-raspberrypi-docker/releases/download/r7.0.14-mongodb-raspberrypi-docker-unofficial/mongodb.ce.pi4.r7.0.14-mongodb-raspberrypi-docker-unofficial.tar.gz
```

Carica l'immagine in Docker:

```bash
docker load --input mongodb.ce.pi4.r7.0.14-mongodb-raspberrypi-docker-unofficial.tar.gz
```

Verifica che l'immagine sia presente:

```bash
docker images
```

---

## Passo 7: Modificare il file `docker-compose.yml`
Apri il file `docker-compose.yml` per modificarlo:

```bash
nano docker-compose.yml
```

Trova la sezione relativa a MongoDB e modifica la riga:

```yaml
image: mongo
```

sostituendola con:

```yaml
image: mongodb-raspberrypi4-unofficial-r7.0.14
```

Salva con **CTRL+O** e chiudi con **CTRL+X**.

---

## Passo 8: Avviare i container
Avvia il servizio:

```bash
docker compose up -d
```

---

## Conclusione
Ora LibreChat dovrebbe essere installato e funzionante. Se incontri problemi, consulta la [documentazione ufficiale](https://docs.librechat.ai).
