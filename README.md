# 🦾 Dashboard NEXUS - Braccio Robotico

Benvenuto nel pannello di controllo NEXUS per il braccio robotico.
Questa applicazione web, sviluppata in Django (Backend) e HTML/Tailwind/JS nativi (Frontend), ti permette di inviare comandi e ricevere dati in tempo reale da un nodo hardware simulato (Raspberry Pi).

---

## 🚀 Come avviare il progetto

Poiché l'applicazione web e il braccio robotico (il simulatore Python) sono due componenti separati che comunicano tra loro, **dovrai aprire due finestre o schede del terminale** per poter avviare sia il server web che il robot vero e proprio.

Entrambi i terminali dovranno essere posizionati all'interno della cartella principale del progetto: `Nexus_Robo_Arm`.

### 1. Avviare il server web (Terminale 1)
Questa è la finestra del terminale in cui gira l'interfaccia utente.

1. Apri un terminale nella cartella `Nexus_Robo_Arm`.
2. Attiva l'ambiente virtuale python digitando:
   ```bash
   source venv/bin/activate
   ```
3. Fai partire il server web con il comando:
   ```bash
   python manage.py runserver 8000
   ```

> ✅ **L'interfaccia è pronta!** Ora puoi aprire il browser (Chrome, Firefox, Safari) e andare all'indirizzo [http://127.0.0.1:8000/](http://127.0.0.1:8000/).

### 2. Avviare il robot simulato (Terminale 2)
Se avvii solo il server web la dashboard funzionerà, ma non riceverà alcun dato né invierà comandi. Lo script di simulazione (`pi_simulator.py`) fa le veci del braccio robotico: si scambia in tempo reale l'angolazione dei motori e le letture di voltaggio con l'app web.

1. Apri un **nuovo terminale o una nuova scheda** (sempre nella cartella `Nexus_Robo_Arm`).
2. Attiva di nuovo l'ambiente virtuale:
   ```bash
   source venv/bin/activate
   ```
3. Avvia lo script che simula il braccio del robot:
   ```bash
   python pi_simulator.py
   ```
   
> ✅ **Connesso!** Vedrai apparire messaggi come `[SYNC OK]` che ti confermano l'invio dei dati alla dashboard in tempo reale.
> Prova adesso ad andare su [http://127.0.0.1:8000/](http://127.0.0.1:8000/): se sposti ad esempio l'asse "J1" e cambi la gradazione, potrai osservare sul terminale del robot i motori che si muovono lentamente per raggiungere i nuovi gradi, e sulla dashboard vedrai aggiornarsi il voltaggio della macchina man mano che compie il movimento.

---

## 🛑 Come spegnere tutto

Per arrestare i due componenti, ti basterà fermare l'esecuzione nei due terminali che hai aperto precedentemente.

1. **Torna al Terminale 1 (Il server web)**
   - Clicca sulla finestra per attivarla.
   - Ripeti il comando **`CTRL + C`** sulla tastiera. Il server web si fermerà.

2. **Torna al Terminale 2 (Il robot)**
   - Clicca sulla finestra.
   - Premi **`CTRL + C`** sulla tastiera per interrompere il programma Python che lo gestisce.

Ora hai spento tutto e le risorse del tuo computer sono state liberate. Puoi chiudere in tranquillità le finestre del terminale.
