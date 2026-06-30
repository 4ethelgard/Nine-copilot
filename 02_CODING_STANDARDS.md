# NINE
# Coding Standards
Versione documento: 1.0

---

# Obiettivo

Questo documento definisce tutte le regole di sviluppo di Nine.

Qualsiasi contributo al progetto deve rispettare integralmente queste regole.

---

# Filosofia

Il codice deve essere:

- leggibile
- semplice
- modulare
- commentato quando necessario
- facilmente estendibile
- facilmente testabile

Scrivere meno codice è preferibile a scrivere codice complicato.

---

# Python

Versione minima:

Python 3.12

---

# Naming

## Classi

PascalCase

Esempi:

MailModule

CalendarModule

NotificationCenter

LearningEngine

---

## Funzioni

snake_case

Esempi

load_modules()

scan_mail()

organize_files()

---

## Variabili

snake_case

Esempi

current_task

mail_label

system_status

---

## Costanti

UPPER_CASE

Esempi

MAX_RETRY

DEFAULT_TIMEOUT

CONFIG_FILE

---

# File

Un file deve avere una responsabilità.

Mai creare file che fanno "un po' di tutto".

---

# Classi

Una classe deve rappresentare un solo concetto.

Se una classe supera circa 400-500 righe va valutata una suddivisione.

---

# Funzioni

Una funzione deve svolgere un solo compito.

Idealmente:

20-40 righe.

Mai oltre le 100 salvo casi eccezionali.

---

# Commenti

Commentare il "perché".

Non il "cosa".

NO

# incremento i

i += 1

SI

# incrementa il contatore dei tentativi
# per evitare retry infiniti

---

# Logger

È vietato usare print().

Qualsiasi messaggio deve passare dal Logger.

---

# Gestione errori

Mai usare

except:

Sempre

except Exception as e:

registrando l'errore.

---

# Hardcoded

È vietato inserire valori configurabili nel codice.

Qualsiasi parametro modificabile appartiene alla cartella config.

---

# Thread

Mai creare thread manualmente senza una reale necessità.

Utilizzare sempre il Task Manager quando possibile.

---

# Eventi

La comunicazione tra moduli avviene esclusivamente tramite Event Bus.

Mai chiamare direttamente un modulo diverso.

---

# Sicurezza

Qualsiasi operazione sui file deve passare dal Security Layer.

---

# AI

Il Brain non modifica direttamente il sistema.

Il Brain prende decisioni.

I moduli eseguono.

---

# Testing

Ogni componente importante deve poter essere testato indipendentemente.

Mai creare dipendenze circolari.

---

# Dipendenze

Preferire sempre la libreria standard.

Aggiungere librerie esterne solo se realmente necessarie.

---

# Performance

Nine deve poter rimanere aperto 24 ore su 24.

Il consumo di RAM e CPU deve essere ridotto al minimo.

---

# Gaming Mode

Se viene rilevato un gioco:

ridurre scansioni

ridurre AI

posticipare task non urgenti

mantenere solo i servizi essenziali

---

# Documentazione

Ogni modulo importante deve avere il proprio documento nella cartella docs.

---

# Git

Commit piccoli.

Messaggi chiari.

Mai caricare dati personali.

Mai caricare password.

Mai caricare API Key.

---

# Qualità

Prima di considerare completato un file chiedersi:

È leggibile?

È modulare?

È riutilizzabile?

È testabile?

Rispetta Project Vision?

Rispetta Architecture?

Se una risposta è NO il file non è pronto.