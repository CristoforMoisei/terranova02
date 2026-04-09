# Schema Logico del Database

| Entità | Attributi principali | Relazioni logiche |
|--------|--------------------|-----------------|
| **User** | `UserID` (PK), `Nome`, `Cognome`, `Email`, `Ruolo`, `Password` | Appartiene a uno o più gruppi (**Group**), può avere molte richieste ferie (**VacationRequest**), può scrivere commenti (**Comment**) |
| **Group** | `GroupID` (PK), `NomeGruppo`, `ResponsabileID` (FK → User) | Ha molti utenti (**User**), ha un responsabile (**User**) |
| **VacationRequest** | `RequestID` (PK), `UserID` (FK → User), `DataInizio`, `DataFine`, `Stato`, `Motivo` | Appartiene a un utente (**User**), può avere molti commenti (**Comment**), soggetta a regole ferie (**Rules**) |
| **Comment** | `CommentID` (PK), `RequestID` (FK → VacationRequest), `UserID` (FK → User), `Testo`, `Data` | Collega un utente (**User**) a una richiesta ferie (**VacationRequest**) |
| **Rules** | `RuleID` (PK), `Periodo`, `MinPresenza`, `GiorniMin`, `GiorniMax`, `ConsecutiviMin`, `ConsecutiviMax`, `PeriodiCritici` | Applicata alle richieste ferie (**VacationRequest**) per validare disponibilità e regole aziendali |
