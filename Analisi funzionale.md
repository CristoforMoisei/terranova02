# ANALISI FUNZIONALE – SISTEMA GESTIONE FERIE

**Team:**
Moisei Cristofor, Bonfanti Riccardo, Marchiella Diego, Tessaro Alessandro

---

# 1. Diagrammi

* Use Case Diagram
* Sequence Diagram

---

# 2. Casi d'Uso Principali

## UC001 – Richiesta Ferie

**Attore principale:** Dipendente

**Pre-condizioni**

* L'utente ha effettuato il login al sistema.

**Post-condizioni**

* La richiesta viene salvata nel database.
* Il manager viene notificato.

### Flusso Principale

1. Il dipendente clicca **"Nuova Richiesta"** dal dashboard.
2. Compila il form inserendo:

   * data di inizio
   * data di fine
   * tipo di ferie.
3. Clicca **"Invia"**.
4. Il sistema valida:

   * le date inserite
   * il saldo ferie disponibile.
5. Il sistema verifica la sovrapposizione nel reparto (**massimo 80% di dipendenti assenti**).
6. Se tutto è valido:

   * salva la richiesta nel database con stato **"Pendente"**
   * invia una **email di notifica al manager**.

### Eccezioni

**E1 – Saldo insufficiente**

Il sistema mostra il messaggio:

```
Ferie non sufficienti
```

**E2 – Sovrapposizione critica**

Il sistema mostra il messaggio:

```
Troppi colleghi in ferie nello stesso periodo
```

---

## UC002 – Gestione Richiesta Ferie

**Attore principale:** Manager

**Pre-condizioni**

* Il manager ha effettuato il login.
* Sono presenti richieste pendenti.

**Post-condizioni**

* La richiesta viene aggiornata a:

  * **Approvata**
  * **Rifiutata**

### Flusso Principale

1. Il manager apre la sezione **"Richieste Team"**.
2. Visualizza la tabella con le richieste pendenti.
3. Clicca sulla richiesta **#123**.
4. Visualizza i dettagli della richiesta.
5. Seleziona:

   * **Approva**
   * oppure **Rifiuta** inserendo una motivazione.
6. Conferma l'operazione.
7. Il sistema:

   * aggiorna lo stato della richiesta
   * aggiorna il saldo ferie del dipendente
   * invia una notifica al dipendente.

### Eccezioni

**E1 – Accesso non autorizzato**

Se il manager tenta di accedere a una richiesta non appartenente al proprio reparto:

```
Accesso negato
```

---

# 5. Modello dei Dati

## Entità Principali

### Users

* id_user (PK)
* nome
* cognome
* email
* ruolo

### Groups

* id_group (PK)
* nome
* descrizione
* id_responsabile (FK)

### Registrazioni

* id_user (PK, FK)
* data
* password

### Commenti

* id_commento (PK)
* id_user (FK)
* testo
* data

---
