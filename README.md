
# Terranova02
## Sistema di Gestione del Calendario Ferie Aziendale

---

## 1. Descrizione del Progetto

Il presente progetto prevede la realizzazione di un sistema informatico per la gestione del calendario ferie aziendale.

L’obiettivo è sviluppare una piattaforma che consenta di:

- Pianificare le ferie nei periodi stabiliti dall’azienda (es. estate, Natale)
- Evitare sovrapposizioni critiche
- Garantire la presenza minima del personale
- Favorire trasparenza tra dipendenti, responsabili e amministrazione
- Automatizzare la validazione delle richieste ferie

Il sistema supporta tre categorie di utenti:
- Dipendenti
- Responsabili di gruppo
- Amministratori aziendali

---

## 2. Obiettivi del Sistema

- Centralizzare la gestione delle ferie
- Applicare regole aziendali configurabili
- Ridurre conflitti tra richieste
- Monitorare la disponibilità del personale
- Fornire uno storico completo delle interazioni

---

## 3. Ruoli del Sistema

| Ruolo | Permessi principali |
|-------|---------------------|
| Dipendente | Inserimento richieste ferie, visualizzazione calendario del gruppo |
| Responsabile di Gruppo | Approvazione/rifiuto richieste, gestione conflitti, inserimento commenti |
| Amministratore Aziendale | Gestione utenti, gruppi, periodi ferie e configurazioni di sistema |

---

## 4. Autenticazione

### Modalità di Accesso

- Login tramite email aziendale e password
- Password salvata mediante hash sicuro
- Nessuna registrazione libera
- Utenti pre-caricati dall’azienda

---

## 5. Modello Dati

### 5.1 Tabella `Users`

| Campo | Tipo | Vincoli |
|-------|------|---------|
| id_user | INT | PK, AUTO_INCREMENT |
| nome | VARCHAR(50) | NOT NULL |
| cognome | VARCHAR(50) | NOT NULL |
| email | VARCHAR(100) | UNIQUE, NOT NULL |
| password_hash | VARCHAR(255) | NOT NULL |
| ruolo | ENUM('DIPENDENTE','RESPONSABILE','ADMIN') | NOT NULL |
| attivo | BOOLEAN | DEFAULT TRUE |

---

### 5.2 Reset Password

Modalità prevista:

- Richiesta reset tramite email aziendale
- Generazione token temporaneo con scadenza

#### Tabella `Password_Reset`

| Campo | Tipo | Vincoli |
|-------|------|---------|
| id_reset | INT | PK |
| id_user | INT | FK → Users(id_user) |
| token | VARCHAR(255) | UNIQUE |
| data_scadenza | DATETIME | NOT NULL |
| utilizzato | BOOLEAN | DEFAULT FALSE |

---

## 6. Organizzazione: Gruppi e Relazioni

Ogni dipendente appartiene ad almeno un gruppo di lavoro.

### Tabella `Groups`

| Campo | Tipo | Vincoli |
|-------|------|---------|
| id_group | INT | PK |
| nome | VARCHAR(100) | NOT NULL |
| id_responsabile | INT | FK → Users(id_user) |

---

### Tabella `User_Groups` (Relazione molti-a-molti)

| Campo | Tipo | Vincoli |
|-------|------|---------|
| id_user | INT | FK → Users(id_user) |
| id_group | INT | FK → Groups(id_group) |
| PRIMARY KEY (id_user, id_group) | | |

---

## 7. Calendario Ferie Condiviso

Dopo il login, l’utente visualizza:

- Le proprie ferie
- Le ferie dei colleghi del gruppo
- I periodi prenotabili
- Eventuali conflitti

### Indicazione Stato Giorni (Interfaccia)

| Stato | Colore suggerito |
|-------|------------------|
| Giorno disponibile | Verde |
| Giorno occupato | Rosso |
| Giorno con conflitto | Giallo |
| Periodo non prenotabile | Grigio |

Il calendario può essere implementato tramite:

- Librerie JavaScript (es. FullCalendar)
- Componenti React o Angular
- Soluzione custom HTML, CSS e JavaScript

---

## 8. Richieste di Ferie

### Tabella `Vacation_Requests`

| Campo | Tipo | Vincoli |
|-------|------|---------|
| id_request | INT | PK |
| id_user | INT | FK → Users(id_user) |
| data_inizio | DATE | NOT NULL |
| data_fine | DATE | NOT NULL |
| stato | ENUM('IN_ATTESA','APPROVATA','RIFIUTATA') | NOT NULL |
| data_richiesta | DATETIME | DEFAULT CURRENT_TIMESTAMP |

---

## 9. Regole di Gestione Ferie

Ogni periodo ferie è configurabile dall’amministrazione aziendale.

### Tabella `Vacation_Periods`

| Campo | Tipo |
|-------|------|
| id_period | INT (PK) |
| nome_periodo | VARCHAR(100) |
| data_inizio | DATE |
| data_fine | DATE |
| min_giorni | INT |
| max_giorni | INT |
| min_consecutivi | INT |
| presenza_minima_percentuale | INT |
| blocco_totale | BOOLEAN |

---

## 10. Validazione delle Richieste

Se una richiesta viola una o più regole:

- Evidenziazione immediata lato client
- Messaggio esplicativo dettagliato
- Blocco automatico o richiesta di revisione

Esempio:

```

Richiesta non valida: numero minimo di giorni consecutivi non rispettato.

```

---

## 11. Gestione Commenti e Comunicazioni

### Tabella `Comments`

| Campo | Tipo |
|-------|------|
| id_comment | INT (PK) |
| id_request | INT (FK) |
| id_autore | INT (FK) |
| testo | TEXT |
| data_commento | DATETIME |

Utilizzata per:

- Richieste di modifica
- Proposte alternative
- Comunicazioni ufficiali

---

## 12. Interfaccia Amministratore

L’amministratore dispone di una sezione dedicata per:

- Creazione e modifica utenti
- Gestione gruppi
- Impostazione periodi ferie
- Configurazione regole
- Monitoraggio disponibilità personale
- Visualizzazione statistiche

---

## 13. Architettura del Sistema

```

Frontend (React / Angular / HTML-CSS-JS)
↓
Backend API REST (NodeJS / PHP / C#)
↓
Database Relazionale (MySQL / PostgreSQL / SQL Server)

```

---

## 14. Obiettivi Formativi

Il progetto consente di sviluppare competenze in:

- Analisi dei requisiti
- Modellazione di database relazionali
- Progettazione architettura software
- Gestione autenticazione e autorizzazioni
- Implementazione di logiche di validazione
- Sviluppo di interfacce web interattive
- Redazione documentazione tecnica
- Pianificazione dei test

---

## 15. Documentazione Richiesta

- Analisi dei requisiti
- Analisi funzionale
- Analisi tecnica
- Schema ER
- Schema logico relazionale
- Piani di test
- Manuale utente
- Manuale di installazione

---

## 16. Criteri di Valutazione

La valutazione si concentra su:

1. Analisi dei requisiti  
2. Modellazione del database  
3. Architettura del sistema  
4. Qualità progettuale  
5. Interfaccia utente  
6. Documentazione tecnica  
7. Processo di sviluppo  
8. Codice (valore aggiunto, non centrale)

---

## 17. Tecnologie Utilizzabili

- Backend: C#, NodeJS, PHP  
- Frontend: HTML, CSS, JavaScript  
- Framework: React, Angular, Vue  
- Database: MySQL, PostgreSQL, SQL Server  
- IDE: Visual Studio, VS Code, Eclipse  

---

## 18. Stato del Progetto

Progetto sviluppato nell’ambito del percorso PCTO  
(Percorsi per le Competenze Trasversali e l’Orientamento).
```
