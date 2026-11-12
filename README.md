# Hydra — firmware

Monorepo del firmware del veicolo a idrogeno **Hydra** (Sapienza).

| Cartella | Contenuto |
|---|---|
| [`dashboard/`](dashboard/) | Cruscotto: ESP32 + display ILI9488 480×320 (velocità, fuel cell, supercap, consumo H₂) |
| [`lib/hydra-protocol/`](lib/hydra-protocol/) | Strutture dati condivise tra le schede (`VehicleData`) |
| [`docs/`](docs/) | Architettura, layout del display, immagini |

Le future schede (es. `telemetry/` per la lettura dei sensori) andranno in una nuova cartella accanto a `dashboard/`, usando `lib/hydra-protocol` per parlare la stessa lingua.

## Requisiti

- [PlatformIO](https://platformio.org/) (estensione VS Code *PlatformIO IDE* oppure `pip install platformio`)
- Opzionale: estensione [Wokwi](https://docs.wokwi.com/vscode/getting-started) per simulare senza hardware

## Compilare

```bash
cd dashboard
pio run -e esp32              # scheda reale
pio run -e esp32 -t upload    # flash via USB
pio run -e wokwi              # poi "Wokwi: Start Simulator" in VS Code
```

In VS Code apri la cartella `dashboard/` (quella con `platformio.ini`) perché PlatformIO la riconosca.

## Regole di lavoro

- Niente push diretti su `main`: si lavora su un branch e si apre una Pull Request.
- La CI compila tutti i target a ogni push/PR: se è rossa, non si fa merge.
- Ogni modifica a `lib/hydra-protocol` va verificata su **tutte** le schede che lo usano.
