# Prototipi

Esperimenti fatti prima del firmware attuale, conservati come riferimento.
**Non sono codice di produzione**: la CI non li compila, e possono essere riscritti o cancellati quando la parte corrispondente entra in `dashboard/` o in una nuova scheda.

Ognuno è un progetto PlatformIO a sé (`pio run -d prototypes/<nome>`).

| Cartella | Scheda | Cosa fa | Stato |
|---|---|---|---|
| [`motor-control-basic/`](motor-control-basic/) | Arduino Uno | Pilota il motore tramite ESC (libreria Servo) con un potenziometro come acceleratore, calcola tensione e potenza | Compila. Mai provato sul motore reale |
| [`motor-control-lcd/`](motor-control-lcd/) | Arduino Uno | Come sopra, più LCD 16x2 con potenza (0–150 kW) e tempo trascorso | Compila. Mai provato sul motore reale |
| [`steering-wheel-lcd/`](steering-wheel-lcd/) | Arduino Mega ADK | Volante: 8 pulsanti con debounce, mostra il tasto premuto su LCD 20x4 I²C | Compila |
| [`steering-wheel-wokwi/`](steering-wheel-wokwi/) | Arduino Uno (Wokwi) | Volante simulato: 8 pulsanti + LCD 20x4, telemetrie simulate (velocità, fuel cell, supercap, corrente motore) | Compila. Simulabile con Wokwi (`diagram.json`) |

## Note

- `motor-control-lcd` usa `malloc` per formattare il tempo: su un Arduino Uno (2 KB di RAM) è da evitare se il codice finisce nel firmware vero.
- `steering-wheel-lcd`: corretto l'indice del tasto stampato (`letters[i]` → `letters[index]`), altrimenti non compilava.
- La logica di debounce e la gestione del volante andranno riprese in `dashboard/src/input/` (oggi `InputManager` è disattivato in `main.cpp`).
