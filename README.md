# 🦾 NEXUS Robotic Arm Dashboard

Benvenuto nel pannello di controllo telemetrico e cinetico bidirezionale NEXUS per il braccio robotico (Ex KINETIC LAB).
Questa web application costruita su Django (Backend) e HTML/Tailwind/JS nativi (Frontend) ti permette di inviare comandi asincroni e ricevere letture sensoristiche in tempo reale da un nodo hardware simulato (Raspberry Pi).

---

## 🚀 Come Avviare il Sistema

Poiché l'applicazione web (Django) e il finto braccio robotico (Simulatore Python) sono due entità completamente distinte che comunicano tramite REST API, **hai bisogno di due finestre di terminale aperte contemporaneamente** per accendere sia il server che il robot vero e proprio.

Entrambi i terminali devono essere aperti dentro la cartella radice del progetto, ovvero la cartella `Nexus_Robo_Arm`.

### 1. Avviare il Backend Django (Finestra Terminale 1)
Questo è il server che serve le pagine HTML ad alta estetica e amministra tutto l'hub di comunicazione.

1. Apri un terminale nella cartella `Nexus_Robo_Arm`.
2. Digita questo comando per **attivare l'ambiente virtuale** (in cui abbiamo installato tutte le librerie Python compatibili):
   ```bash
   source venv/bin/activate
   ```
3. Appena vedi `(venv)` a sinistra del terminale, fai partire concretamente il server digitando:
   ```bash
   python manage.py runserver 8000
   ```

> ✅ **Il pannello web ora è online.** Puoi aprire Chrome/Safari e recarti all'indirizzo [http://127.0.0.1:8000/](http://127.0.0.1:8000/) sul tuo computer locale!

### 2. Avviare il "Raspberry Pi" Simulata (Finestra Terminale 2)
Se ti limiti ad accendere Django, il sistema funziona ma è inanimato, nessun macchinario raccoglierà la "forza/coppia", i "gradi cinetici" o scaricherà i task. Lo script di simulazione (`pi_simulator.py`) è un robot che gira in background e genera telemetria vitale super realistica con l'api web.

1. Apri una **nuova scheda/nuova finestra del terminale** (rimanendo sempre puntato alla cartella `Nexus_Robo_Arm`).
2. Anche qui devi accendere l'ambiente Python:
   ```bash
   source venv/bin/activate
   ```
3. Avvia lo script hardware del finto braccio:
   ```bash
   python pi_simulator.py
   ```
   
> ✅ **Tutto Connesso!** Noto subito nel terminale scorrere messaggi ad alto ritmo del tipo `[SYNC OK] ... | Gripper: DISENGAGED...`. Significa che ha trovato la dashboard web e sta costantemente calcolando e interpolando i motori. Se ora tu ti rechi all'indirizzo [http://127.0.0.1:8000/](http://127.0.0.1:8000/) e sposti velocemente l'angolo di posizionamento dell'asse "J1" sul sito web della Dashboard da 140° a 360°, potrai osservare lo script nel Terminale 2 che riceve l'input muovere lentamente i giunti stampandoli man mano fino al raggiungimento di 360°, insieme all'aumento dinamico del Voltaggio/Torque che vedrai riflettersi dal vivo sulla Dashboard. Fantastico!

---

## 🛑 Come Fermare e Spegnere il Sistema

Fermare e spegnere tutto è un gesto semplicissimo e fulmineo usando la tua tastiera. Per arrestare definitivamente tutto devi letteralmente "Uccidere" le mansioni in esecuzione nei due terminali aperti.

1. **Torna sul Terminale/Scheda 1 (Quello in cui gira Django Web App)**
   - Clicca col mouse all'interno della nera finestra o tab del terminale per attivarla.
   - Sulla tastiera esegui la scorciatoia combinando **`CTRL + C`** e aspetta per una frazione di secondo. Questo lancerà un segnale noto come `SIGINT (Interrupt)` forzando il tuo computer ad arrestare il server Django definitivamente. Se ora aggiorni il browser web vedrai spaccarsi o scadere la connessione su Chrome.

2. **Torna sul Terminale/Scheda 2 (Quello dello Script Simulato pi_simulator)**
   - Anche qui abbi l'accortezza di prendere il focus cliccando col mouse.
   - Ripeti la sacra shortcut premendo **`CTRL + C`**. Il robot e la logica interpolarizzata finirà di stampare di botto gettando un `KeyboardInterrupt`.

Il progetto Nexos Robo Arm e la porta 8000 del tuo iMac (macOS) sono tornati allo stato riposato. Niente consumerà più il tuo computer. Potrai infine chiudere con la spunta rossa le finestre.
