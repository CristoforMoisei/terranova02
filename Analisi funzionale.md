# ANALISI FUNZIONALE - SISTEMA GESTIONE XXXX

TEAM: _________  

Diagrammi 

**Use Case Diagram**
**Sequence Diagram**


## 2. CASI D'USO PRINCIPALI

### UC001: 

**Attore principale**: Dipendente 
**Pre-condizioni**: Login effettuato
**Post-condizioni**: Richiesta salvata, Manager notificata

**Flusso principale**:

1. Clicca "Nuova Richiesta" dal Dashboard
2. Compila form: date inizio/fine, tipo ferie
3. Clicca "Invia" → Sistema valida date e saldo
4. Verifica sovrapposizioni reparto (<80%)
5. Salva DB stato="Pendente", invia email Manager

**Eccezioni**: 

- E1: Saldo insufficiente → Alert "Ferie non sufficienti"
- E2: Sovrapposizione critica → "Troppi colleghi in ferie"

### UC002: 

**Attore principale**: Manager 
**Pre-condizioni**: Login, richieste pendenti
**Post-condizioni**: Stato "Approvata/Rifiutata"

**Flusso principale**:

1. Apre "Richieste Team" → Tabella pendenti
2. Clicca richiesta #123 → Vede dettagli
3. Seleziona "Approva" o "Rifiuta + motivazione"
4. Conferma → Aggiorna saldo ferie, notifica Dipendente

**Eccezioni**: E1: Fuori reparto → Accesso negato

### UC003: 

**Attore principale**: HR 
**Pre-condizioni**: Login HR
**Post-condizioni**: CSV esportato

**Flusso principale**:

1. Apre "Report Reparto" → Seleziona mese/reparto
2. Vede grafico torta + tabella dettagli
3. Clicca "Esporta CSV" → Download file

**Eccezioni**: E1: Nessun dato → "Report vuoto"


## 2. SEQUENZA

actor "Dipendente Mario" as D
participant Sistema as S
participant DB as DB
participant Email as E
participant "Manager Anna" as M

D -> S: login(email,pass)
S -> DB: validateUser()
DB --> S: OK + saldo=22gg
S --> D: Token Ok

D -> S: POST /richieste {15/07-19/07}
S -> DB: checkSovrapposizioni(IT) alt <80% reparto
S -> DB: INSERT (stato='Pendente')
S -> E: notificaManager()
E -> M: "Nuova richiesta #456"
S --> D: SUCCESS 
S --> D: ERROR sovrapposizione


## 3. MODELLI DATI

**Entità Principali**:
- Utenti: id, matricola, nome, cognome, reparto, ruolo, email, ferie_residue (int)
- Richieste: id, utente_id(FK), data_richiesta, data_inizio, data_fine, stato, manager_id(FK)
- Reparti: id, nome, max_assenti_simultanei (15% totale)




