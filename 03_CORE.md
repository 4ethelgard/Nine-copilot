# NINE
# Core System
Versione documento: 1.0

---

# Obiettivo

Il Core rappresenta il cuore di Nine.

È l'unico componente che conosce l'intero sistema.

Il suo compito non è prendere decisioni, ma coordinare il funzionamento di tutti gli altri componenti.

---

# Principio fondamentale

Il Core NON contiene intelligenza artificiale.

Il Core NON interpreta il linguaggio.

Il Core NON organizza mail.

Il Core NON organizza file.

Il Core coordina solamente.

---

# Componenti

Il Core è composto dai seguenti elementi.

## Nine

Classe principale.

Responsabilità:

- avvio del programma
- inizializzazione
- ciclo principale
- arresto

---

## Kernel

È il direttore d'orchestra.

Coordina:

- Modules
- Services
- Event Bus
- Scheduler
- Task Manager

Il Kernel non prende decisioni.

---

## Lifecycle Manager

Gestisce il ciclo di vita del sistema.

Stati:

BOOT

STARTING

READY

BUSY

PAUSED

SHUTDOWN

ERROR

Ogni componente può conoscere lo stato corrente.

---

## Config Manager

Carica tutta la configurazione.

Legge solamente.

Mai logica.

---

## Logger

Ogni componente utilizza un logger dedicato.

Formato consigliato:

[ORA]

[LIVELLO]

[MODULO]

Messaggio

Esempio:

[14:22:31]

[INFO]

[MAIL]

Scanning mailbox...

---

## Event Bus

È il sistema nervoso di Nine.

Qualsiasi componente può pubblicare eventi.

Qualsiasi componente può ascoltare eventi.

Un evento contiene:

- id
- timestamp
- mittente
- tipo
- payload
- priorità

Esempio:

mail_received

payload

{
    account: "gmail",
    sender: "...",
    subject: "...",
}

---

## Command Bus

Differenza fondamentale.

Event Bus

↓

qualcosa è successo

Command Bus

↓

qualcosa deve essere eseguito

Esempio.

Speech:

"Sposta questa mail"

↓

Brain

↓

Command Bus

↓

Mail Module

---

## Module Loader

Carica automaticamente tutti i moduli presenti.

Non devono essere registrati manualmente.

In futuro sarà sufficiente aggiungere una cartella modulo.

---

## Service Loader

Carica automaticamente tutti i servizi.

---

## Scheduler

Genera eventi temporali.

Esempi:

ogni 30 minuti

ogni ora

all'avvio

ogni lunedì

mai direttamente le operazioni.

---

## Task Manager

Qualsiasi operazione importante diventa un Task.

Stati possibili:

WAITING

RUNNING

PAUSED

COMPLETED

FAILED

CANCELLED

RETRYING

Ogni Task possiede priorità.

---

## Startup Manager

All'avvio:

1 Config

2 Logger

3 Database

4 Services

5 Modules

6 Brain

7 Speech

8 Phone

9 Automation

10 READY

---

## Shutdown Manager

Procedura inversa.

Salvataggio dati.

Chiusura servizi.

Backup se necessario.

---

## Watchdog

Controlla continuamente che:

i servizi siano vivi

i moduli rispondano

non ci siano loop infiniti

In caso contrario tenta un riavvio del componente.

---

# Comunicazione

È vietato questo.

Speech

↓

Mail

Mail

↓

Calendar

Calendar

↓

Files

Corretto.

Speech

↓

Brain

↓

Kernel

↓

Command Bus

↓

Modulo

---

# Bootstrap

Il primo avvio di Nine è speciale.

Il Core deve riconoscerlo.

Durante il primo avvio vengono creati:

config

database

cartelle

chiavi

cache

backup iniziale

---

# Modalità operative

Il Core supporta tre modalità.

NORMAL

Operatività completa.

LOW_RESOURCE

Riduce il consumo.

GAMING

Riduce scansioni.

Riduce AI.

Posticipa attività non urgenti.

---

# Gestione errori

Il crash di un modulo NON deve fermare Nine.

Il Core registra l'errore.

Disabilita temporaneamente il modulo.

Notifica l'utente.

Continua a funzionare.

---

# Regola finale

Il Core è l'unico componente autorizzato a conoscere l'intera architettura del progetto.

Tutti gli altri componenti conoscono esclusivamente ciò che serve al proprio funzionamento.