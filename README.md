# TRA PYTHON E ARDUINO
## Nampy vs Micropython

Un confronto dettagliato basato sulle fonti:
1. Architettura e Modalità di Esecuzione
Nanpy: Funziona secondo una logica Master-Slave. Arduino non è un dispositivo indipendente, ma agisce come uno "slave" che esegue continuamente i comandi impartiti dal computer (il "master") tramite un protocollo seriale
. Il codice Python risiede e gira interamente sul computer
.
MicroPython: Permette di caricare ed eseguire gli script Python direttamente sulla scheda
. In questo caso, il microcontrollore non ha bisogno di un computer esterno per funzionare una volta che il codice è stato caricato
.
2. Autonomia e Connessione
Nanpy: Richiede una connessione seriale costante tra Arduino e il PC
. Se il cavo viene scollegato, Arduino smette di ricevere istruzioni e non può operare in autonomia
.
MicroPython: La scheda è autonoma. Si utilizza il computer solo per scrivere e trasferire i file .py tramite appositi editor (come Arduino Lab per MicroPython o OpenMV IDE), dopodiché la scheda può funzionare indipendentemente
.
3. Performance e Limiti
Nanpy: Il principale svantaggio è il collo di bottiglia rappresentato dalla velocità della comunicazione seriale, che può limitare le applicazioni che richiedono un'esecuzione molto rapida
. È però eccellente per l'acquisizione dati dove l'analisi complessa è lasciata al PC
.
MicroPython: Essendo un'implementazione ottimizzata per girare direttamente sull'hardware, non soffre dei limiti della latenza seriale per l'esecuzione del codice
.
4. Hardware Supportato
Nanpy: È ampiamente utilizzato con schede classiche come Arduino Uno
.
MicroPython: È supportato ufficialmente solo da una selezione di schede più recenti e potenti, tra cui:
Serie Nano: Nano ESP32 (usata per il corso MicroPython 101), Nano 33 BLE Sense, Nano RP2040 Connect
.
Serie Portenta: Portenta H7, Portenta C33
.
Altre: Arduino GIGA R1 WiFi, Nicla Vision e Arduino Opta
.
5. Strumenti di Sviluppo
Nanpy: Si installa tramite pip e può essere utilizzato con qualsiasi IDE Python standard, come Spyder
. Richiede il caricamento del firmware Nanpy.ino tramite l'IDE di Arduino
.
MicroPython: Richiede l'installazione di un firmware specifico (spesso in formato .dfu o .hex) e l'uso di editor dedicati come Arduino Lab for MicroPython o OpenMV IDE per la visione artificiale

<details>
  <summary>Prima soluzione -> Numpy</summary>

# Python + Arduino: Controllo Hardware con Nanpy

**Nanpy** è un progetto che permette di programmare e controllare una scheda Arduino utilizzando il linguaggio **Python** attraverso una connessione seriale tra la scheda e il computer.

## 1. Cos'è Nanpy?
Nanpy non è un singolo software, ma l'unione di due componenti fondamentali:
*   **Un protocollo seriale:** Permette l'invio di comandi specifici dal computer verso Arduino.
*   **Una libreria Python:** Fornisce le interfacce necessarie per sfruttare tale protocollo in modo semplice all'interno di script Python.

In questa configurazione, Arduino opera come uno **slave**: non è più un dispositivo indipendente, ma esegue continuamente i comandi impartiti dal computer (master) tramite Python.

## 2. Vantaggi e Svantaggi

### Vantaggi
*   **Semplificazione dello sviluppo:** Non è necessario scrivere e caricare nuovo codice Arduino per ogni variazione dell'esperimento; si può gestire tutto da un singolo programma Python.
*   **Potenza di calcolo:** Permette di utilizzare Arduino come scheda di acquisizione dati, lasciando l'analisi complessa alla potenza di calcolo del computer e alle librerie scientifiche di Python,.
*   **Integrazione:** È ideale per la creazione di laboratori di fisica e sistemi di analisi dati in tempo reale,.

### Svantaggi
*   **Dipendenza dal computer:** Arduino non può funzionare in autonomia poiché necessita della connessione seriale costante per ricevere istruzioni.
*   **Velocità di comunicazione:** La connessione seriale può diventare un collo di bottiglia se l'applicazione richiede un'esecuzione estremamente rapida dei comandi.

## 3. Guida all'Installazione

### Passo 1: Installazione del Firmware su Arduino
Per permettere ad Arduino di "capire" i comandi Python, è necessario installare il **Nanpy-Firmware**:
1.  Scaricare il firmware dal repository ufficiale.
2.  Individuare la cartella **Nanpy** e aprire il file **Nanpy.ino** all'interno dell'IDE di Arduino.
3.  Caricare il programma sulla scheda (è possibile ignorare eventuali warning di compilazione, purché l'upload vada a buon fine).

### Passo 2: Installazione della Libreria Python
La libreria può essere installata tramite il package manager standard di Python:
*   **Da linea di comando:** `pip install nanpy`.
*   **All'interno di Spyder (IDE):** Eseguire `!pip install nanpy` direttamente nella console iPython.

## 4. Esempio Pratico: Blink
Una volta configurato l'ambiente, è possibile creare un semplice script (es. `blink.py`) per far lampeggiare il LED integrato della scheda,. 
*   Durante l'esecuzione, si noteranno i **LED TX e RX** di Arduino lampeggiare, indicando la comunicazione seriale attiva tra il computer e la scheda.
*   Per interrompere l'esecuzione del programma, è sufficiente utilizzare la combinazione di tasti **CTRL-C**.

## 5. Applicazioni Comuni
La soluzione Nanpy è particolarmente indicata per,,:
*   **Laboratori di Fisica:** Acquisizione dati e analisi del moto o di circuiti (es. Circuito RC).
*   **Sensori:** Gestione di sensori di temperatura e umidità come la famiglia **DHT**.
*   **Didattica:** Esperimenti scientifici complessi (es. misurazione della costante di Planck) semplificati dall'uso di Python,.

---

*Nota: Questa documentazione è tratta dai tutorial di Ludovico Russo sull'integrazione hardware tra Python e Arduino.*
</details>
<details>
<summary>Micropython e arduino</summary>

## MicroPython su Arduino: Guida alla Soluzione Ufficiale
Arduino ha introdotto il linguaggio Python come opzione aggiuntiva per la programmazione dei propri microcontrollori, scegliendo **MicroPython** come piattaforma di riferimento
. A differenza della soluzione **Nanpy** (dove Arduino funge da slave), MicroPython permette al codice di girare direttamente sulla scheda.
1. Cos'è MicroPython per Arduino?
MicroPython è un'implementazione efficiente del linguaggio Python 3, ottimizzata per girare su microcontrollori
. Arduino contribuisce attivamente al progetto ufficiale supportando il repository upstream e integrando il supporto per le proprie schede
.
2. Hardware Supportato
Non tutte le schede Arduino supportano MicroPython. La documentazione elenca specificamente i seguenti modelli compatibili
:
Serie Nano: **Nano ESP32, Nano 33 BLE Sense, Nano RP2040 Connect**.
Serie Portenta: **Portenta H7, Portenta C33**.
Altre schede professionali: **Arduino GIGA R1 WiFi, Arduino Nicla Vision, Arduino Opta**.
Il corso introduttivo "MicroPython 101" utilizza specificamente la scheda Arduino Nano ESP32 come hardware di riferimento
.
3. **Ambienti di Sviluppo** (Editor)
Per caricare script MicroPython sulle schede, Arduino propone due editor principali
:
**Arduino Lab for MicroPython**: Un editor sperimentale e leggero, ideale per la scrittura di codice MicroPython standard
.
**OpenMV IDE**: Un editor specializzato per il firmware OpenMV, orientato alla machine vision (visione artificiale) e al machine learning
.
4. Installazione e Configurazione
Installazione del Firmware
Prima di poter eseguire script Python, è necessario caricare il firmware corretto sulla scheda
. Esistono due modalità principali
:
Arduino MicroPython Installer: Uno strumento raccomandato per un'installazione rapida e semplice.
Installazione Manuale: È possibile scaricare manualmente versioni specifiche del firmware (in formato .dfu o .hex) a seconda della stabilità richiesta (versioni stable o preview)
.
**Caricamento del Codice**
Una volta installato il firmware, si utilizza un editor compatibile per connettersi alla scheda e trasferire i file .py
.
5. **Risorse Didattiche e Progetti**

Arduino offre diverse risorse per iniziare
:
**MicroPython 101**: Un corso strutturato che guida l'utente attraverso capitoli di apprendimento ed esercizi pratici
.
Esempi per Scheda: Raccolte di codice per sfruttare le caratteristiche specifiche di ogni modello (es. GIGA R1 WiFi)
.
Progetti **Plug-and-Play**: Progetti completi di codice e schemi circuitali pronti all'uso
.
6. **OpenMV e Visione Artificiale**
Per applicazioni avanzate, Arduino supporta il firmware OpenMV, basato anch'esso su MicroPython
. Questo ecosistema include un editor dedicato e permette di implementare soluzioni di visione artificiale e apprendimento automatico direttamente sull'hardware Arduino
.

--------------------------------------------------------------------------------
Nota: Queste informazioni sono tratte dalla documentazione ufficiale Arduino aggiornata al 2026
</details>
