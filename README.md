# Sistema di Gestione del Calendario Ferie Aziendale

![Status](https://img.shields.io/badge/status-in%20development-blue)

![Backend](https://img.shields.io/badge/backend-php-green)
![Frontend](https://img.shields.io/badge/frontend-HTML%2FCSS%2FJS-orange)
![Database](https://img.shields.io/badge/database-MySQL-lightgrey)

## Descrizione del Progetto

Il progetto prevede la realizzazione di un sistema informatico per la gestione del calendario ferie annuale dei dipendenti di un’azienda.

L’obiettivo è sviluppare una piattaforma web che consenta:

- La pianificazione delle ferie nei periodi stabiliti dall’azienda (es. periodo estivo, festività natalizie).
- Il rispetto delle regole aziendali relative alla disponibilità minima del personale.
- La gestione dei conflitti tra richieste.
- La comunicazione tra dipendenti, responsabili di gruppo e amministrazione.

---

## Obiettivi Funzionali

Il sistema dovrà permettere:

### 1. Autenticazione e gestione utenti

- Accesso tramite login.
- Utenti pre-caricati dall’azienda (assenza di registrazione libera).
- Gestione ruoli: Dipendente, Responsabile di gruppo, Amministratore.
- Possibilità di reset credenziali.

### 2. Gestione gruppi e ruoli

- Ogni dipendente appartiene ad almeno un gruppo di lavoro.
- Ogni gruppo ha un responsabile.
- Il responsabile può:
  - Visualizzare le richieste del proprio team
  - Approvare o rifiutare richieste
  - Gestire conflitti
  - Comunicare tramite sistema di commenti

### 3. Calendario ferie condiviso

- Visualizzazione:
  - Ferie personali
  - Ferie dei colleghi del gruppo
  - Periodi prenotabili
- Evidenziazione giorni:
  - Disponibili
  - In conflitto
  - Non prenotabili

### 4. Regole aziendali configurabili

Per ogni periodo ferie è possibile definire:

- Finestra temporale
- Presenza minima per ruolo
- Numero minimo/massimo di giorni prenotabili
- Numero minimo/massimo di giorni consecutivi
- Periodi critici bloccati

### 5. Gestione richieste e approvazioni

- Invio richiesta ferie
- Segnalazione conflitti
- Approvazione, rifiuto o richiesta modifica
- Storico comunicazioni tramite tabella Comments

### 6. Area amministrativa

L’amministratore può:

- Gestire utenti, gruppi e ruoli
- Configurare periodi ferie
- Impostare regole e criteri di priorità
- Monitorare disponibilità del personale

---

## Architettura del Sistema

Il progetto è strutturato secondo un’architettura client-server:

- Frontend: interfaccia web per utenti e amministratori
- Backend: gestione logica applicativa e validazione regole
- Database relazionale: gestione dati strutturati

---

## Modellazione Database

Il sistema prevede un database relazionale con entità principali quali:

- User
- Group
- Comment
- Registrazione

---

## Tecnologie Utilizzate

Le tecnologie sono:

- Backend: 
- Frontend:
- Framework:
- Database: 
- Ambiente di sviluppo: Visual Studio Code

---

## Autori

Bonfanti, Marchiella, Moisei, Tessaro.

![Status](https://img.shields.io/badge/status-in%20development-blue)
![Database](https://img.shields.io/badge/database-MySQL-orange)
