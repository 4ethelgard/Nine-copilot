# NINE
# Software Architecture
Versione documento: 1.0

---

# Obiettivo

Questo documento descrive l'architettura definitiva di Nine.

L'architettura è considerata congelata.

Una volta iniziato lo sviluppo della v1.0 non dovrà più essere modificata.

Nuove funzionalità dovranno essere aggiunte esclusivamente tramite nuovi moduli o plugin.

---

# Filosofia

Nine è progettato come un piccolo sistema operativo.

Ogni componente possiede una sola responsabilità.

Nessun componente deve conoscere il funzionamento interno degli altri.

La comunicazione avviene esclusivamente attraverso il Kernel e l'Event Bus.

---

# Livelli del sistema

L'intero progetto è diviso in sette livelli.

┌───────────────────────────────┐
│        USER                   │
└──────────────┬────────────────┘
               │
┌──────────────▼────────────────┐
│ INTERFACES                    │
│ Speech - Phone - UI - API     │
└──────────────┬────────────────┘
               │
┌──────────────▼────────────────┐
│ BRAIN                         │
│ Comprensione e decisioni       │
└──────────────┬────────────────┘
               │
┌──────────────▼────────────────┐
│ KERNEL                        │
│ Coordinazione generale         │
└──────────────┬────────────────┘
               │
┌──────────────▼────────────────┐
│ SERVICES                      │
│ Sicurezza, Task, Queue...     │
└──────────────┬────────────────┘
               │
┌──────────────▼────────────────┐
│ MODULES                       │
│ Mail, Files, Calendar...      │
└──────────────┬────────────────┘
               │
┌──────────────▼────────────────┐
│ STORAGE                       │
│ Database, Cache, Config        │
└───────────────────────────────┘

---

# Responsabilità

## User

L'utente comunica solamente con Nine.

Mai direttamente con i moduli.

---

## Interfaces

Le interfacce raccolgono input.

Non prendono decisioni.

Non modificano dati.

Trasmettono solamente richieste al Brain.

---

## Brain

Il Brain interpreta il linguaggio.

Comprende il contesto.

Decide quale operazione eseguire.

Il Brain NON esegue operazioni.

---

## Kernel

Il Kernel coordina tutto il sistema.

Gestisce:

- Event Bus

- caricamento moduli

- caricamento servizi

- task

- lifecycle

- startup

- shutdown

Il Kernel non contiene logica AI.

---

## Services

I Services sono componenti sempre attivi.

Esempi:

- Scheduler

- Queue

- Security

- Notifications

- Resource Monitor

- Automation

I Services non parlano direttamente con l'utente.

---

## Modules

Ogni modulo gestisce una singola funzionalità.

Mail.

Calendario.

Files.

Speech.

Phone.

Ogni modulo deve essere completamente indipendente.

---

## Storage

Lo Storage contiene esclusivamente dati.

Mai logica.

Mai decisioni.

---

# Comunicazione

I componenti NON si chiamano direttamente.

Esempio scorretto:

Mail -> Brain

Brain -> Calendar

Calendar -> Files

Questo è vietato.

---

La comunicazione corretta è:

Mail

↓

Event Bus

↓

Kernel

↓

Brain

↓

Kernel

↓

Modulo destinazione

---

# Event Bus

Ogni evento del sistema viene pubblicato.

Chi è interessato lo ascolta.

Esempi:

mail_received

calendar_updated

file_moved

notification_requested

task_completed

phone_connected

voice_command

system_idle

game_detected

startup_completed

---

# Task Manager

Qualsiasi operazione importante diventa un Task.

Un Task possiede:

- id

- priorità

- stato

- creatore

- timestamp

- progresso

- risultato

Il Task Manager permette:

pausa

ripresa

annullamento

retry

monitoraggio

---

# Scheduler

Lo Scheduler NON svolge operazioni.

Lo Scheduler dice solamente:

"Esegui questo Task alle 10:00"

oppure

"Ogni 30 minuti"

---

# Automation Engine

L'Automation Engine riceve gli eventi dello Scheduler.

Decide quali controlli automatici avviare.

Esempi:

controllo mail

controllo calendario

controllo desktop

pulizia cache

backup

---

# Resource Manager

Il Resource Manager controlla continuamente:

CPU

GPU

RAM

Spazio Disco

Processi

Giochi

Fullscreen

Carico generale

Se il sistema è occupato,

Nine riduce automaticamente il proprio utilizzo.

---

# Security Layer

Ogni richiesta viene verificata.

Prima di modificare qualsiasi file:

↓

Security

↓

Permesso

↓

Operazione

In caso contrario:

Operazione rifiutata.

---

# Learning

L'apprendimento è separato dalla logica.

Ogni modulo produce Feedback.

Il Learning Engine analizza i feedback.

Aggiorna le preferenze dell'utente.

Mai il contrario.

---

# Database

Il Database è la memoria permanente.

Contiene:

Preferenze

Storico

Regole

Statistiche

Modelli

Queue

Configurazioni

Mai codice.

---

# Configurazione

Ogni impostazione modificabile deve essere salvata nella cartella config.

Mai valori hardcoded nel codice.

---

# Logging

Ogni componente possiede il proprio logger.

Mai usare print().

Sempre Logger.

---

# Error Handling

Ogni errore deve essere:

registrato

contestualizzato

gestito

Mai terminare Nine per un errore di un modulo.

---

# Startup

L'avvio segue SEMPRE questo ordine.

1. Config

2. Logger

3. Database

4. Kernel

5. Services

6. Modules

7. Brain

8. Interfaces

9. Automation

10. Sistema pronto

Mai cambiare questo ordine.

---

# Shutdown

Lo spegnimento avviene nell'ordine inverso.

---

# Estensioni future

Nuove funzionalità devono essere implementate esclusivamente tramite:

nuovi moduli

nuovi servizi

plugin

Mai modificando il Kernel.

---

# Regola finale

Il Kernel è il cuore del sistema.

Il Brain è il cervello.

I Services sono gli organi.

I Modules sono gli strumenti.

Lo Storage è la memoria.

Nessun componente deve assumere il ruolo di un altro.