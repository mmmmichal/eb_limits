# Karty – Limity

| Súhrn | Zdroje pre správu limitov platobných kariet v&nbsp;_Banking Services API_. |
| ----- | --------------------------------------------------------------------------- |
| Stav  | `Final` |

[[_TOC_]]

---

## Popis

Zdroje pre správu limitov platobných kariet v&nbsp;_Banking Services API_ poskytujú funkcionalitu na **zobrazenie a úpravu používania limitov debetných platobných kariet**.

Endpointy umožňujú klientovi:
- získať prehľad aktuálne nastavených limitov,
- meniť vybrané limity (výbery z bankomatu, POS platby, internetové platby, celkový obrat na karte),

a to v rámci hraníc definovaných bankou a konfiguráciou kartového produktu.

Tieto endpointy sú určené **výhradne pre debetné karty**.  
Kreditné, virtuálne a business karty sú **mimo rozsahu** a riešia sa samostatnými API.

---

## API Endpointy

### Karty – Limity

#### GET /v1/cards/{cardIdentifier}/limits – Získanie limitov debetnej karty

Vráti aktuálne nastavené limity pre konkrétnu debetnú kartu identifikovanú pomocou `cardIdentifier`.

---

#### PUT /v1/cards/{cardIdentifier}/limits – Úprava limitov debetnej karty

Upravuje nastaviteľné limity pre konkrétnu debetnú kartu identifikovanú pomocou `cardIdentifier`.

---

## Request

Autorizácia: Autorizačný token (OAuth 2.0 Bearer – Base64 kódovaná HTTP hlavička) poskytnutý riešením Federated Login.

### Path parametre

| Názov parametra | Povinnosť | Typ parametra | Dátový typ | Význam |
|----------------|-----------|---------------|------------|--------|
| cardIdentifier | Y | path | string | **cardTokenisedPan** – jedinečný identifikátor karty, ktorý je zároveň aj maskovaným PANom<br>- regex: `^[0-9]{6}[a-zA-Z]{6}[0-9]{4}$` |

---

### Hlavičky

| Hlavička | Povinná | Popis |
| ------- | ------- | ----- |
| Authorization | Áno | OAuth 2.0 Bearer token |
| Content-Type | Áno | `application/json` |

---


## GET – Response

### Response Body

| Atribút | Typ | Povinné | Popis |
| ------ | --- | ------- | ----- |
| id | String | Áno | ID limitu |
| type | String | Áno | Typ limitu |
| period | String | Áno | Perióda limitu |
| limit | Money | Áno | Aktuálne nastavená hodnota limitu |

---

### Príklad GET response

```json
[
  {
    "id": "LIMIT_123456",
    "type": "ATM",
    "period": "1D",
    "limit": {
      "amount": 300,
      "currency": "EUR"
    }
  }
]
``
