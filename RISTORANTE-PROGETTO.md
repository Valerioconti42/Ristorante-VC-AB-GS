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
```
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
```
**UTENTE CON RISTORANTE:**
```
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
```
---
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
```

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
```
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
```
---
