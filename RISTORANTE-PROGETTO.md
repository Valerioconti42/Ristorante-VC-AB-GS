## PROGETTO 1: SISTEMA DI RECENSIONI PER RISTORANTI

## 📝 DESCRIZIONE PROGETTO
Applicazione per la gestione di recensioni di ristoranti. 
Gli utenti possono registrarsi e accedere, pubblicare recensioni con voti e immagini, filtrare i ristoranti cucina, prezzo e valutazione.
I proprietari di ristoranti possono registrarsi e accedere, inserire il ristorante nel sistema.

**Funzionalità principali:**
- Registrazione/login per utenti e proprietari di ristoranti
- Pubblicazione di recensioni con voti e immagini
- Filtrare per tipo di cucina, prezzo e valutazione
- Leggere la classifica dei migliori ristoranti basata sulle recensioni

---

## FASE 1: COMPRENSIONE DEL DOMINIO

### 1.1 Identificazione delle Entità Principali

**Analisi:**
```
ENTITÀ IDENTIFICATE:
- Ristorante (id, nome, capienza, orari, posizione_via, media_recensioni)
- Recensione (id, voto, immagine, autore, data, ristorante_recensito)
- Utente (id, email, password, recensioni_pubblicate, ristoranti_gestiti)
```

**Relazioni:**
```
- Un utente può pubblicare più recensioni (0:N)
- Una recensione deve essere pubblicata da uno e uno solo utente (1:1)
- Una recensione deve appartenere a uno e uno solo ristorante (1:1)
- Un ristorante può avere più recensione (0:N)
- Un utente può creare più ristoranti (0:N)
- Un utente può modificare più ristoranti (0:N)
- Un ristorante può essere modificato da uno e un solo utente (1:1)
- Un ristorante può essere creato da uno e un solo utente (1:1)

```

---

### 1.2 Identificazione degli Utenti e Ruoli

**Ruoli identificati:**
```
RUOLO: Utente
Permessi:
  - Registrarsi/Login
  - Visualizzare classifica ristoranti 
  - Filtrare ristoranti
  - Pubblicare, cancellare e modificare recensioni
  - Creare un ristorante
  - Modificare il proprio profilo

RUOLO: Utente con ristorante
Permessi:
  - Login
  - Visualizzare classifica ristoranti 
  - Filtrare ristoranti
  - Pubblicare, cancellare e modificare recensioni
  - Creare un ristorante
  - Modificare il proprio ristorante
  - Modificare il proprio profilo

```

---

## FASE 2: ANALISI DEI CASI D'USO

### 2.1 Elenco delle Operazioni per Entità

**UTENTE:**
1. Registrarsi nel sistema
2. Effettuare login
3. Visualizzare classifica ristoranti
4. Visualizzare dettagli di un ristotante
5. Pubblicare una recensione
6. Modificare una recensione già esistente
7. Eliminare una recensione già esistente
8. Filtrati i ristoranti
9. Creare un ristorante
10. Modificare il proprio profilo

**UTENTE CON RISTORANTE:**
1. Effettuare login
2. Visualizzare classifica ristoranti
3. Visualizzare dettagli di un ristotante
4. Pubblicare una recensione
5. Modificare una recensione già esistente
6. Eliminare una recensione già esistente
7. Filtrati i ristoranti
8. Creare un ristorante
9. Modifica del proprio ristorante 
10. Modificare il proprio profilo
---
```

### 2.2 Flussi di Business

**FLUSSO 1: Pubblicare recensione**
```
1. Utente effettua login
2. Utente apre una finestra di una nuova recensione
3. Utente inserisce dati della recensione, di cui voto, immagine, testo e ristorante recensito
4. Utente invia la recensione
5. Sistema invia notifica che la recensione è stata inserita oppure dà un errore se dei dati sono mancanti
6. Utente ora può modificare o eliminare la recensione

```

**FLUSSO 2: Creare ristorante**
```
1. Utente effetua login
2. Utente apre una finestra per creare un nuovo ristorante
3. Utente scrive i dati/attributi del ristorante
4. Utente pubblica ristorante
5. Sistema invia notifica che il ristorante è stato pubblicato oppure dà un errore se dei dati sono mancanti
6. Utente ora può modificare il ristorante

```

---

## FASE 3: PROGETTAZIONE DELLE RISORSE REST

### 3.1 Identificazione delle Risorse

**Risorse base:**
```
- /Utenti
- /Recensioni
- /Ristoranti

**Risorse annidate:**
```
- /Utenti/Registrazione
- /Utenti/Login
- /Ristoranti/Creare
- /RistorantI/Modificare
- /Recensioni/Creare
- /Recensioni/Modificare
- /Ristoranti/Classifica
- /Ristoranti/Classifica/Filtro
```

**Risorse speciali:**
```
- /auth/registrazione
- /auth/login
```

---

### 3.2 Mappatura Operazioni → Metodi HTTP

| Operazione | Metodo HTTP | Endpoint | Accesso |
|------------|-------------|----------|---------|
| Registrazione utente | POST | `/api/v1/auth/registrazione` | Pubblico |
| Login | POST | `/api/v1/auth/login` | Pubblico |
| Logout | POST | `/api/v1/auth/logout` | Autenticato |
| Classifica ristoranti | GET | `/api/v1/ristoranti` | Pubblico/Autenticato |
| Informazioni ristorante | GET | `/api/v1/ristoranti/{id}` | Pubblico/Autenticato |
| Creare recensione | POST | `/api/v1/recensioni` | Recensione |
| Modificare recensione | PUT/PATCH | `/api/v1/recensioni` | Recensione (proprie) |
| Cancella recensione | DELETE | `/api/v1/recensioni/{id}` | Recensione (proprie) |
| Lista recensioni | GET | `/api/v1/ristoranti/{id}/recensioni` | Recensioni |
| Creare ristorante | POST | `/api/v1/ristoranti/crea` | Ristorante |
| Modifica ristorante | PATCH | `/api/v1/ristoranti/{id}/modifca` | Ristorante |

---

## FASE 4: DEFINIZIONE DEI DTO

### 4.1 Esempi Request Body

**POST /api/v1/auth/registrazione**
```json
{
  "nome": "Mario",
  "cognome": "Rossi",
  "email": "mario.rossi@example.com",
  "telefono": "+39 123 456 7890",
  "codice_fiscale": "RSSMRA80A01H501U",
  "data_nascita": "1980-01-01",
  "password": "passwordSicura123!",
  "ruolo": "paziente"
}
```

**POST /api/v1/appuntamenti**
```json
{
  "medico_id": 5,
  "data": "2025-02-15",
  "ora": "14:30",
  "motivo_visita": "Controllo annuale",
  "durata_minuti": 30
}
```

**POST /api/v1/medici/{id}/disponibilita**
```json
{
  "giorno_settimana": "lunedi",
  "orario_inizio": "09:00",
  "orario_fine": "13:00",
  "attivo": true
}
```

---

### 4.2 Esempi Response Body

**GET /api/v1/medici/{id}**
```json
{
  "id": 5,
  "nome": "Dr. Giovanni",
  "cognome": "Bianchi",
  "email": "g.bianchi@studio.it",
  "specializzazione": "Cardiologia",
  "numero_albo": "12345",
  "studio": {
    "id": 2,
    "nome": "Studio Medico Centro",
    "indirizzo": "Via Roma 10, Milano"
  },
  "links": {
    "self": "/api/v1/medici/5",
    "disponibilita": "/api/v1/medici/5/disponibilita",
    "appuntamenti": "/api/v1/medici/5/appuntamenti"
  }
}
```

**GET /api/v1/medici/{id}/disponibilita?data=2025-02-15**
```json
{
  "medico": {
    "id": 5,
    "nome": "Dr. Giovanni",
    "cognome": "Bianchi"
  },
  "data": "2025-02-15",
  "orari_disponibili": [
    {
      "ora": "09:00",
      "disponibile": true
    },
    {
      "ora": "09:30",
      "disponibile": false,
      "motivo": "già prenotato"
    },
    {
      "ora": "10:00",
      "disponibile": true
    }
    // ... altri orari
  ]
}
```

**GET /api/v1/dashboard/medico**
```json
{
  "medico": {
    "id": 5,
    "nome": "Dr. Giovanni",
    "cognome": "Bianchi"
  },
  "data_odierna": "2025-01-15",
  "appuntamenti_oggi": [
    {
      "id": 123,
      "ora": "10:00",
      "paziente": {
        "id": 10,
        "nome": "Mario",
        "cognome": "Rossi"
      },
      "motivo_visita": "Controllo",
      "stato": "confermato"
    }
  ],
  "appuntamenti_settimana": 12,
  "appuntamenti_in_attesa": 3
}
```

---

## FASE 5: GESTIONE ERRORI

**Esempio risposta errore:**
```json
{
  "error": {
    "code": "SLOT_NON_DISPONIBILE",
    "message": "L'orario selezionato non è più disponibile",
    "details": {
      "medico_id": 5,
      "data": "2025-02-15",
      "ora": "09:30",
      "alternativa_suggerita": {
        "ora": "10:00",
        "disponibile": true
      }
    },
    "timestamp": "2025-01-15T14:30:00Z"
  }
}
```

---

## FASE 6: AUTENTICAZIONE

**POST /api/v1/auth/login**
```json
Request:
{
  "email": "mario.rossi@example.com",
  "password": "passwordSicura123!"
}

Response (200 OK):
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "expires_in": 3600,
  "user": {
    "id": 10,
    "nome": "Mario",
    "cognome": "Rossi",
    "email": "mario.rossi@example.com",
    "ruolo": "paziente"
  }
}
```

---

## CHECKLIST FINALE

Per questo progetto, verificate di aver definito:

### ✅ Analisi
- [ ] Tutte le entità principali sono state identificate
- [ ] Le relazioni tra entità sono state mappate
- [ ] I ruoli utente sono stati definiti con permessi chiari

### ✅ Progettazione API
- [ ] Tutte le operazioni sono mappate a endpoint REST
- [ ] I metodi HTTP sono corretti per ogni operazione
- [ ] Gli endpoint seguono convenzioni REST (plurali, gerarchici)
- [ ] I parametri query sono definiti per filtri e ricerca

### ✅ Dati
- [ ] Le strutture Request body sono definite per ogni POST/PUT/PATCH
- [ ] Le strutture Response body sono definite per ogni endpoint
- [ ] Le validazioni sui dati sono specificate
- [ ] I codici di stato HTTP sono appropriati

### ✅ Sicurezza
- [ ] L'autenticazione è richiesta dove necessario
- [ ] Le autorizzazioni per ruolo sono definite
- [ ] Gli endpoint pubblici vs privati sono identificati

### ✅ Funzionalità Speciali
- [ ] Le notifiche sono progettate
- [ ] La ricerca e i filtri sono implementabili
- [ ] Le relazioni tra risorse sono rappresentate (link o embedded)
- [ ] La paginazione è prevista per liste lunghe

---

**Buon lavoro nella definizione delle vostre API REST! 🚀**

