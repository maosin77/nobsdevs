# n8n Local Setup

Lokalna instancja n8n z Docker Compose.

## Struktura projektu

```
n8n-local/
├── .env                 # konfiguracja środowiska
├── Dockerfile          # obraz n8n
├── docker-compose.yml   # orchestracja kontenerów
└── data/               # dane n8n (workflowy, credentials, baza)
```

## Szybki start

1. **Uruchom Docker Desktop**

2. **Wystartuj n8n:**
   ```bash
   docker compose up -d
   ```

3. **Otwórz aplikację:**
   http://localhost:5678

## Komendy

```bash
# Start
docker compose up -d

# Zatrzymanie
docker compose down

# Podgląd logów
docker compose logs -f

# Aktualizacja do najnowszej wersji
docker compose pull
docker compose up -d
```

## Backup

```bash
# Zatrzymaj i zarchiwizuj
docker compose down
tar -czf backup-n8n-$(date +%F).tar.gz data
```

## Konfiguracja

Główne ustawienia w `.env`:
- `N8N_ENCRYPTION_KEY` - klucz szyfrowania (zachowaj!)
- `TZ` - strefa czasowa

## Dane

Wszystkie workflowy, credentials i baza SQLite zapisują się w folderze `./data/`.

## Przykładowy workflow

W repozytorium znajduje się `youtube-transcript-workflow.json` - workflow do ekstraktowania transkryptów z filmów YouTube.

**Import workflow:**
1. Otwórz n8n (http://localhost:5678)
2. Kliknij "+" → "Import from file"
3. Wybierz `youtube-transcript-workflow.json`
4. Uzupełnij swój klucz RapidAPI w węźle `extractTranscript`

## HTTPS/Produkcja

Do wystawienia publicznie dodaj reverse proxy (Caddy/Nginx) z certyfikatem SSL.