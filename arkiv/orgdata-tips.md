---
layout: default
title: "Tips & Tricks" 
parent: "Orgdata"
nav_order: 3
---

### Omkode flere input til felles output fra samme kolonne med `RE`

Bruk av *TYPE* `KB` i kodebok for omkoding kan bare håndtere en-til-en omkoding.
Men hvis det er behov for å omkode flere verdier til en felles verdi i samme
kolonne, kan man bruke *TYPE* `RE` dvs. regulæruttryk eller [rex](https://rex.r-lib.org/ "rex"), istedenfor.
For eksample å omkode kolonne *INNVKAT* med verdi 1, 2, 3 eller 5, til 8 kan
defineres som følgende. Alle eksempler nedenfor gir samme resultat.

Med `RE` ved bruk av [rex](https://rex.r-lib.org/ "rex"):

| LESID | KOL     | TYPE | FRA            | TIL |
|-------|---------|:----:|----------------|:---:|
| ver1  | INNVKAT | RE   | rex(or(1:3,5)) | 8   |

Med `RE` ved bruk av regulæruttryk:

| LESID | KOL     | TYPE | FRA        | TIL |
|-------|---------|:----:|------------|:---:|
| ver1  | INNVKAT | RE   | 1\|2\|3\|5 | 8   |

Alle boolean symboler kan brukes her dvs. `|` og `&` for ELLER og OG.


Med standard `KB` omkoding dvs. 1-til-1 omkoding:

| LESID | KOL     | TYPE | FRA | TIL |
|-------|---------|:----:|:---:|:---:|
| ver1  | INNVKAT | KB   | 1   | 8   |
| ver1  | INNVKAT | KB   | 2   | 8   |
| ver1  | INNVKAT | KB   | 3   | 8   |
| ver1  | INNVKAT | KB   | 5   | 8   |

