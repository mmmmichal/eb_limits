```mermaid
gantt
    title Delivery plan 2026 - dopad za Daily banking
    dateFormat  YYYY-MM-DD
    axisFormat  %d.%m.%Y

    section Fázy
    Analýza                         :a1, 2026-04-01, 2026-06-01
    Development                     :d1, 2026-05-01, 2026-08-01
    Testing                         :t1, 2026-07-15, 2026-09-01

    section Nasadenie na prostredia (milestones)
    FAT (deploy)                    :milestone, m1, 2026-06-01, 0d
    SIT (deploy)                    :milestone, m2, 2026-08-01, 0d
    UAT (deploy)                    :milestone, m3, 2026-09-15, 0d
    PROD (deploy)                   :milestone, m4, 2026-10-01, 0d
```
