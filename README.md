# 🌅 Blueprint Home Assistant - Luci Giardino Intelligenti

Un blueprint avanzato per Home Assistant che gestisce automaticamente l'illuminazione del giardino basandosi sul tramonto e sui sensori di movimento.

## ✨ Caratteristiche

- **Accensione automatica al tramonto**: Le luci si accendono automaticamente quando il sole scende sotto una percentuale configurabile di elevazione
- **Rilevamento movimento**: Aumenta automaticamente l'intensità delle luci quando viene rilevato movimento
- **Configurazione flessibile**: Personalizza facilmente tutti i parametri tramite l'interfaccia di Home Assistant
- **Ottimizzazione energetica**: Gestione intelligente dell'illuminazione per ridurre i consumi

## 🏠 Requisiti

- Home Assistant 2023.4 o superiore
- Sensore sole configurato (automatico in HA)
- Almeno una luce compatibile con dimming
- Almeno un sensore di movimento (opzionale per funzionalità avanzate)

## 🚀 Installazione

### Metodo 1: Import diretto
1. Copia l'URL del blueprint: 
   ```
   https://github.com/[il-tuo-username]/ha-garden-lights-blueprint/blob/main/garden_lights_automation.yaml
   ```
2. Vai in Home Assistant → Impostazioni → Automazioni e Scene → Blueprint
3. Clicca su "Importa Blueprint" e incolla l'URL

### Metodo 2: Download manuale
1. Scarica il file `garden_lights_automation.yaml`
2. Copialo nella cartella `config/blueprints/automation/` di Home Assistant
3. Riavvia Home Assistant
4. Il blueprint apparirà nella lista dei blueprint disponibili

## ⚙️ Configurazione

### Parametri principali:

| Parametro | Tipo | Default | Descrizione |
|-----------|------|---------|-------------|
| **Luci giardino** | Entity | Richiesto | Seleziona le luci del giardino da controllare |
| **Sensore movimento** | Entity | Opzionale | Sensore PIR o similare per rilevare presenza |
| **Elevazione sole per accensione** | Numero | -6° | Gradi sotto orizzonte per accensione automatica |
| **Luminosità base** | Numero | 30% | Intensità luci durante ore serali |
| **Luminosità con movimento** | Numero | 80% | Intensità quando rilevato movimento |
| **Durata luminosità alta** | Tempo | 5 min | Quanto mantenere alta intensità dopo movimento |
| **Orario spegnimento notturno** | Tempo | 23:30 | Ora di spegnimento automatico |

### Esempio di configurazione:

```yaml
# Configurazione tipica per giardino residenziale
Luci: light.giardino_faretti
Sensore movimento: binary_sensor.pir_giardino
Elevazione sole: -8
Luminosità base: 25%
Luminosità movimento: 85%
Durata alta intensità: 7 minuti
Spegnimento: 00:00
```

## 🔧 Personalizzazione avanzata

Il blueprint supporta anche:

- **Condizioni meteo**: Possibilità di aumentare luminosità con pioggia/nebbia
- **Giorni della settimana**: Comportamenti diversi per weekend/giorni feriali  
- **Stagionalità**: Adattamento automatico ai cambi di stagione
- **Zone multiple**: Gestione di diverse aree del giardino

## 📊 Logica di funzionamento

```
🌅 Tramonto (elevazione < soglia)
    ├── ✅ Accendi luci al 30%
    │
🚶 Movimento rilevato
    ├── ⬆️ Aumenta luminosità al 80%
    ├── ⏱️ Avvia timer 5 minuti
    │
🕐 Timer scaduto SENZA nuovo movimento  
    ├── ⬇️ Riduci luminosità al 30%
    │
🌙 Ora spegnimento (23:30)
    ├── ❌ Spegni tutte le luci
```

## 🐛 Risoluzione problemi

### Le luci non si accendono al tramonto
- Verifica che il sensore sole sia configurato
- Controlla l'elevazione impostata (prova valori tra -6° e -10°)
- Assicurati che le luci siano raggiungibili

### Il sensore movimento non funziona
- Controlla lo stato del sensore negli strumenti sviluppatore
- Verifica che il sensore rilevi correttamente il movimento
- Controlla i log di Home Assistant per errori

### Consumo energetico alto
- Riduci la luminosità base (prova 20-25%)
- Imposta un orario di spegnimento più precoce
- Considera l'uso di luci LED ad alta efficienza

## 🤝 Contribuire

I contributi sono benvenuti! Per contribuire:

1. Fork del repository
2. Crea un branch per la tua feature (`git checkout -b feature/AmazingFeature`)
3. Commit delle modifiche (`git commit -m 'Add some AmazingFeature'`)
4. Push al branch (`git push origin feature/AmazingFeature`)
5. Apri una Pull Request

### Idee per miglioramenti:
- Integrazione con sensori meteo
- Supporto per luci colorate (RGB)
- Modalità vacanza/assenza
- Integrazione con sistemi di sicurezza

## 📝 Changelog

### v1.0.0 (Data corrente)
- ✨ Prima versione del blueprint
- ⚡ Accensione automatica al tramonto
- 🚶 Rilevamento movimento con aumento luminosità
- ⏰ Spegnimento programmato notturno

## 📄 Licenza

Questo progetto è distribuito sotto licenza MIT. Vedi il file `LICENSE` per maggiori dettagli.

## ⭐ Supporto

Se questo blueprint ti è utile:
- ⭐ Lascia una stella al repository
- 🐛 Segnala bug nelle Issues
- 💡 Proponi nuove funzionalità
- 📢 Condividi con la comunità Home Assistant

---

**Nota**: Questo blueprint è stato testato con Home Assistant 2024.x. Per versioni precedenti potrebbero essere necessarie modifiche minori.

## 🏷️ Tags

`home-assistant` `blueprint` `automation` `garden` `lights` `motion-sensor` `sunset` `smart-home` `domotica`