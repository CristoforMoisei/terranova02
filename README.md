# terranova02
- Sistema di Gestione del Calendario Ferie Aziendale

Progetto PCTO

- Descrizione del Progetto

Il presente progetto consiste nella realizzazione di un sistema informatico per la gestione del calendario ferie aziendale.

L'obiettivo è sviluppare una piattaforma che consenta di:

Pianificare le ferie nei periodi stabiliti dall’azienda (es. estate, Natale)

Evitare sovrapposizioni critiche

Garantire la presenza minima del personale

Favorire trasparenza tra dipendenti, responsabili e amministrazione

Automatizzare la validazione delle richieste ferie

Il sistema è progettato per supportare dipendenti, responsabili di gruppo e amministratori aziendali con funzionalità e permessi differenti.

- Obiettivi del Sistema

Centralizzare la gestione delle ferie

Applicare regole aziendali configurabili

Ridurre conflitti tra richieste

Monitorare disponibilità del personale

Fornire uno storico completo delle interazioni

- Ruoli del Sistema
Ruolo	Permessi principali
Dipendente	Inserimento richieste ferie, visualizzazione calendario gruppo
Responsabile di Gruppo	Approvazione/rifiuto richieste, gestione conflitti, commenti
Amministratore Aziendale	Gestione utenti, gruppi, periodi ferie, regole
- Autenticazione
Modalità di Accesso

Login tramite email aziendale + password

Password salvata con hash sicuro

Nessuna registrazione libera

Utenti pre-caricati dall’azienda

- Tabella Users
Campo	Tipo	Vincoli
id_user	INT	PK, AUTO_INCREMENT
nome	VARCHAR(50)	NOT NULL
cognome	VARCHAR(50)	NOT NULL
email	VARCHAR(100)	UNIQUE, NOT NULL
password_hash	VARCHAR(255)	NOT NULL
ruolo	ENUM	('DIPENDENTE','RESPONSABILE','ADMIN')
attivo	BOOLEAN	DEFAULT TRUE
- Reset Password

Modalità prevista:

Richiesta reset tramite email aziendale

Generazione token temporaneo

Tabella Password_Reset
Campo	Tipo	Vincoli
id_reset	INT	PK
id_user	INT	FK → Users
token	VARCHAR(255)	UNIQUE
data_scadenza	DATETIME	NOT NULL
utilizzato	BOOLEAN	DEFAULT FALSE
- Organizzazione: Gruppi e Relazioni

Ogni dipendente appartiene ad almeno un gruppo.

- Tabelle Coinvolte
Groups
Campo	Tipo	Vincoli
id_group	INT	PK
nome	VARCHAR(100)	NOT NULL
id_responsabile	INT	FK → Users
User_Groups (Relazione molti-a-molti)
Campo	Tipo	Vincoli
id_user	INT	FK → Users
id_group	INT	FK → Groups
PRIMARY KEY (id_user, id_group)		
- Calendario Ferie Condiviso

Dopo il login, l’utente visualizza:

Le proprie ferie

Le ferie dei colleghi del gruppo

I periodi prenotabili

Eventuali conflitti

- Indicazione Stato Giorni (UI)
Stato	Colore suggerito
Giorno disponibile	🟢 Verde
Giorno occupato	🔴 Rosso
Giorno con conflitto	🟡 Giallo
Periodo non prenotabile	⚫ Grigio

Il calendario può essere realizzato tramite:

Librerie JavaScript (es. FullCalendar)

Componenti React / Angular

Calendario custom HTML + JS

- Tabella Vacation_Requests
Campo	Tipo	Vincoli
id_request	INT	PK
id_user	INT	FK → Users
data_inizio	DATE	NOT NULL
data_fine	DATE	NOT NULL
stato	ENUM	('IN_ATTESA','APPROVATA','RIFIUTATA')
data_richiesta	DATETIME	DEFAULT CURRENT_TIMESTAMP
- Regole di Gestione Ferie

Ogni periodo ferie ha regole configurabili.

- Tabella Vacation_Periods
Campo	Tipo
id_period	INT PK
nome_periodo	VARCHAR(100)
data_inizio	DATE
data_fine	DATE
min_giorni	INT
max_giorni	INT
min_consecutivi	INT
presenza_minima_percentuale	INT
blocco_totale	BOOLEAN
- Validazione Richieste

Se una richiesta viola una regola:

Evidenziazione immediata lato client

Messaggio esplicativo

Blocco automatico o richiesta revisione

Esempio messaggio:

"Richiesta non valida: numero minimo giorni consecutivi non rispettato"

- Gestione Commenti e Comunicazioni
Tabella Comments
Campo	Tipo
id_comment	INT PK
id_request	INT FK
id_autore	INT FK
testo	TEXT
data_commento	DATETIME

Utilizzata per:

Richieste di modifica

Proposte alternative

Comunicazioni ufficiali

- Interfaccia Amministratore

Funzionalità:

Creazione/modifica utenti

Gestione gruppi

Impostazione periodi ferie

Configurazione regole

Monitoraggio disponibilità personale

Visualizzazione statistiche

- Architettura del Sistema

Possibile architettura:

Frontend (React / Angular / HTML-CSS-JS)
⬇
Backend API REST (NodeJS / PHP / C#)
⬇
Database Relazionale (MySQL / PostgreSQL / SQL Server)

- Obiettivi Formativi

Il progetto permette agli studenti di sviluppare competenze in:

Analisi dei requisiti

Modellazione database relazionale

Progettazione architettura software

Gestione autenticazione

Implementazione validazioni

Sviluppo interfacce web interattive

Redazione documentazione tecnica

Pianificazione test

- Documentazione Richiesta

Analisi dei requisiti

Analisi funzionale

Analisi tecnica

Schema ER

Schema logico relazionale

Piani di test

Manuale utente

Manuale di installazione

- Criteri di Valutazione

La valutazione si concentra su:

Analisi dei requisiti

Modellazione database

Architettura del sistema

Qualità progettuale

Interfaccia utente

Documentazione tecnica

Processo di sviluppo

Codice (valore aggiunto, non centrale)

- Tecnologie Utilizzabili

Backend: C#, NodeJS, PHP

Frontend: HTML, CSS, JavaScript

Framework: React, Angular, Vue

Database: MySQL, PostgreSQL, SQL Server

IDE: Visual Studio, VS Code, Eclipse

- Stato del Progetto

Progetto sviluppato nell’ambito del percorso PCTO (Percorsi per le Competenze Trasversali e l’Orientamento).
