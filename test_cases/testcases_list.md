# Zoznam test cases – Úprava limitov v digitálnych kanáloch

---
[[_TOC_]]
## Smoke / End‑to‑End (E2E)

| TC-ID | Scenár | Kanál | Produkt | Cieľ |
|-----|------|------|--------|-----|
| TC-E2E-01 | Zmena limitu – úspešná | Web | Debetná karta | Overiť happy path |
| TC-E2E-02 | Zmena limitu – úspešná | Mobil | Debetná karta | Overiť mobilný flow |
| TC-E2E-03 | Zmena limitu – úspešná | Web | Osobný účet | Overiť E2E pre účet |
| TC-E2E-04 | Zmena limitu – úspešná | Mobil | Osobný účet | Overiť mobilný variant |
| TC-E2E-05 | Dostupnosť služby 24/7 | Web / Mobil | Karta / Účet | Overiť dostupnosť mimo pracovných hodín |

---

## Navigácia & dostupnosť funkcie

| TC-ID | Scenár | Očakávanie |
|-----|------|-----------|
| TC-UI-01 | Viditeľnosť funkcie pre retail | Retail vidí „Limity“ |
| TC-UI-02 | Korporátny klient | Funkcia skrytá / zakázaná |
| TC-UI-03 | Zobrazenie aktuálnych limitov | Hodnoty zhodné s backendom |
| TC-UI-04 | Frontend validácie | Neplatné hodnoty neakceptované |

---

## Autorizácia & podpisovanie

| TC-ID | Scenár | Očakávanie |
|-----|------|-----------|
| TC-AUTH-01 | Úspešný podpis | Limit zmenený |
| TC-AUTH-02 | Úspešný podpis – mobil | Korektný mobile security flow |
| TC-AUTH-03 | Zrušenie podpisu | Zmena sa neuloží |
| TC-AUTH-04 | Neplatný podpis | Operácia zamietnutá |
| TC-AUTH-05 | Chýba bezpečnostný predmet | Zmena nepovolená |
| TC-AUTH-06 | Timeout podpisu | Limit nezmenený |

---

## Biznis pravidlá limitov

| TC-ID | Scenár | Očakávanie |
|-----|------|-----------|
| TC-BIZ-01 | Zmena v min/max rozsahu | Zmena prejde |
| TC-BIZ-02 | Nad maximálny limit | Zamietnuté |
| TC-BIZ-03 | Pod minimálny limit / 0 | Podľa pravidiel |
| TC-BIZ-04 | Viac limitov naraz | Podľa pravidiel |
| TC-BIZ-05 | Periodicita limitu | Správne uložená |
| TC-BIZ-06 | Mena limitu | Správna mena a formát |

---

## Neobmedzený počet zmien

| TC-ID | Scenár | Očakávanie |
|-----|------|-----------|
| TC-NOLIM-01 | Opakované zmeny | Bez limitu, platí posledná |
| TC-NOLIM-02 | Súbežná zmena (web + mobil) | Bez nekonzistencie |
| TC-NOLIM-03 | Rovnaká hodnota | Bez chyby, korektný audit |

---

## Chybové a stavové scenáre

| TC-ID | Scenár | Očakávanie |
|-----|------|-----------|
| TC-ERR-01 | Backend nedostupný | Hláška, žiadny pád |
| TC-ERR-02 | Chyba pri uložení | Zmena sa nepotvrdí |
| TC-ERR-03 | Čiastočné zlyhanie | Rollback alebo jasný výsledok |
| TC-ERR-04 | Retry po chybe | Bez duplicitných zápisov |

---

## Produktové obmedzenia

| TC-ID | Scenár | Očakávanie |
|-----|------|-----------|
| TC-PROD-01 | Karta blokovaná / expirovaná | Správne obmedzenie |
| TC-PROD-02 | Účet v špeciálnom stave | Zmena zakázaná / povolená |
| TC-PROD-03 | Viac produktov | Zmena správneho objektu |
| TC-PROD-04 | Produkt bez limitov | Korektná UI hláška |

---

## Bezpečnosť & audit

| TC-ID | Scenár | Očakávanie |
|-----|------|-----------|
| TC-SEC-01 | Audit trail | Kompletné logovanie |
| TC-SEC-02 | Cudzí produkt | Access denied (403) |
| TC-SEC-03 | Session timeout | Vyžaduje re-auth |
| TC-SEC-04 | Manipulácia payloadu | Backend odmietne |
| TC-SEC-05 | GDPR / PII | Žiadne citlivé údaje v logoch |

---

## Notifikácie & UX

| TC-ID | Scenár | Očakávanie |
|-----|------|-----------|
| TC-NOTIF-01 | Potvrdenie zmeny | UI + push / záznam v profile pre pobočku a KC |
| TC-NOTIF-02 | História zmien | Správne záznamy |
| TC-NOTIF-03 | Jazykové verzie | Konzistentné texty |

---

## Všeobecné

| TC-ID | Scenár | Očakávanie |
|-----|------|-----------|
| TC-NF-01 | Výkon | SLA dodržané |
| TC-NF-02 | Stabilita | Bez degradácie |
| TC-NF-03 | Dostupnosť | Jasná komunikácia výpadkov |