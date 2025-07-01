
# Protokol CRA (1.0)

### Struktura zprávy
```
┌────────┬──────────┬─────────────┬──────────────────┬───────────┬───────────┬────────────┐
│ Start  │ Hlavička │ ID zařízení │ Velikost Dat     │ Data      │ Kontrolní │ Konec      │
│ (1 B)  │ (1 B)    │ (4 B)       │ dat (2 B)        │ data (n B)│ součet    │ (1 B)      │
│        │          │             │                  │           │ (1 B)     │            │
└────────┴──────────┴─────────────┴──────────────────┴───────────┴───────────┴────────────┘
```
Celková délka = 1 + 1 + 4 + 2 + n + 1 + 1 = n + 10 bytů

#### Popis polí

| Pole             | Velikost | Hodnota/Poznámka                                       |
|------------------|----------|--------------------------------------------------------|
| Start marker     | 1 B      | `0xAB` – značící začátek rámce                         |
| Hlavička         | 1 B      | Struktura zprávy                                       |
| ID zařízení      | 4 B      | prefix `0xAC` + sériové číslo zařízení                 |
| Velikost dat     | 2 B      | Nepodepsané 16bitové (LE): délka dat (max 65535)       |
| Data             | n B      | Binární data                                           |
| Kontrolní součet | 1 B      | XOR všech bytů od `Hlavičky` po konec `Užitečných dat` |
| Konec marker     | 1 B      | `0xBA` – značící konec rámce                           |

### Bitové schéma hlavičky
```
 ┌──7──┬──6──┬──5──┬──4──┬──3──┬──2──┬──1──┬──0──┐
 │  v1 │  v0 │  t1 │  t0 │  p3 │  p2 │  p1 │  p0 │
 └─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘
```

- v1–v0: verze protokolu `(0b01 → 0x40)`
- t1–t0: typ zprávy     `(0b01 → 0x10)`
- p3–p0: typ užitečných dat `(0b0001 → 0x01)`

### Příklad hex-dumpu

Pro `deviceId = 0x123456` a `payload = "TEST"` (ASCII 54 45 53 54):

| Pole                | Byty (hex)                                                   |
|---------------------|--------------------------------------------------------------|
| Start               | `AB`                                                         |
| Hlavička            | `51`                                                         |
| Prefix ID zařízení  | `AC`                                                         |
| ID – nejnižší byt   | `56`                                                         |
| ID – prostřední byt | `34`                                                         |
| ID – nejvyšší byt   | `12`                                                         |
| Délka užitečných    | `04` `00` (4)                                                |
| Užitečná data       | `54 45 53 54`                                                |
| Kontrolní součet    | `16` – XOR hodnot 51, AC, 56, 34, 12, 04, 00, 54, 45, 53, 54 |
| Konec               | `BA`                                                         |

### Validace a chybové stavy

- **Ověření začátečního/konečného markeru** – rámec musí začínat `0xAB` a končit `0xBA`
- **Ověření kontrolního součtu** – pokud XOR(hlavička…užitečná data) ≠ kontrolní součet, zpráva je neplatná.
