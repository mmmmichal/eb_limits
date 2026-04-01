---

## API Endpointy

### Účty – Limity

#### GET /v1/accounts/{accId}/limits  
**Zoznam limitov účtu**

Vracia zoznam všetkých dostupných a nastaviteľných limitov pre konkrétny účet identifikovaný pomocou `accId`.

Endpoint slúži na:
- zobrazenie aktuálne nastavených hodnôt limitov,
- zistenie maximálnych a minimálnych povolených hodnôt,
- overenie stavu limitov (aktívny, čakajúci, zamietnutý).

---

## Request

### Autorizácia

OAuth 2.0 Bearer token (Base64 kódovaná HTTP hlavička) poskytnutý riešením Federated Login.

---

### Path parametre

| Názov parametra | Povinnosť | Typ | Popis |
|---------------|-----------|-----|------|
| accId | Áno | string | Jedinečný identifikátor účtu |

---

### Query parametre (voliteľné)

| Parameter | Typ | Povinný | Popis |
|---------|-----|--------|------|
| type | String | Nie | Filtrovanie podľa typu limitu |
| period | String | Nie | Filtrovanie podľa periódy (`1D`, `7D`, `30D`) |

---

### Hlavičky

| Hlavička | Povinná | Popis |
|--------|--------|------|
| Authorization | Áno | OAuth 2.0 Bearer token |
| Accept | Áno | `application/json` |

---

## Response

### Úspešná odpoveď

#### HTTP 200 OK

Zoznam limitov viazaných na účet.

---

### Response Body

Response obsahuje **pole objektov limitov**.

#### Atribúty položky zoznamu

| Atribút | Typ | Popis |
|-------|-----|------|
| id | String | Identifikátor limitu |
| type | String | Typ limitu účtu |
| period | String | Perióda platnosti limitu |
| limit | Money | Aktuálne nastavená hodnota limitu |
| status | String | Stav limitu |

---

### Príklad response body

```json
[
  {
    "id": "LIMIT_123456",
    "type": "OUTGOING_PAYMENT",
    "period": "1D",
    "limit": {
      "amount": 3000,
      "currency": "EUR"
    },
    "status": "ACTIVE"
  },
  {
    "id": "LIMIT_789012",
    "type": "INSTANT_PAYMENT",
    "period": "1D",
    "limit": {
      "amount": 1000,
      "currency": "EUR"
    },
    "status": "PENDING"
  }
]