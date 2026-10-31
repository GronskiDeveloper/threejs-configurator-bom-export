# Praca AI-first: notatki dla tego repo

Trzymam ten plik w repozytorium, bo buduję z Claude Code (Anthropic) i chcę, żeby podział „człowiek/AI" był widoczny z drzewa plików, a nie deklarowany w README.

## Podział pracy człowiek vs AI

| Warstwa | Kto zrobił | Dlaczego tak |
|---|---|---|
| Pomysł i teza repo | **Człowiek**. Teza: konfigurator nie kończy się na widoku 3D, musi wypluć to, co fabryka zbuduje. BOM i CSV to ten brakujący krok. | To miejsce, gdzie najwięcej konfiguratorów się zatrzymuje, a klient potem przepisuje wymiary do cutlisty ręcznie. Stamtad biora sie bledy. |
| Reguly BOM (co jest czescia, ile sztuk, jaki rozmiar) | **Człowiek** | Grubosc plyty 18 mm, sciana z wnekami, plecy z HDF, kolki co polka x4, okleina liczona w metrach biezacych. To wiedza o tym, jak sie meble faktycznie robi, nie o kodzie. |
| Geometria i funkcja `bom()` z tych samych liczb | **Design człowieka, kod AI** | Zdecydowalem, ze geometria i lista czesci maja plynac z jednego zrodla (szer/wys/gl/polki). Claude przepisal to na mesze i wiersze tabeli. Pilnowalem, zeby rozmiary w BOM zgadzaly sie z tym, co widac. |
| Setup sceny, eksport CSV, UI | **Draft AI, decyzje człowieka** | Environment i cien jak w reszcie serii. Eksport CSV celowo bez biblioteki, zwykly Blob. |

## Co zweryfikowałem przed wypchnięciem

- Otworzyłem `index.html` w przeglądarce: szafka przebudowuje się przy skrajnych wymiarach, BOM przelicza wiersze i sztuki, zero błędów w konsoli.
- Wyeksportowalem CSV i otworzylem go: naglowki i wiersze poprawne, rozmiary w mm zgodne z suwakami.
- Puściłem detektor anty-wzorców na `index.html`. Czysto.

## Znane pułapki dla następnej iteracji AI

- **BOM musi plynac z tych samych liczb co geometria.** Jesli nastepny przebieg zacznie wpisywac rozmiary czesci na sztywno obok geometrii, rozjada sie przy pierwszej zmianie wymiaru. Jedno zrodlo prawdy.
- To starter edukacyjny: zalozenia (18 mm plyta, proste ciecia) sa uproszczone. Prawdziwy cutlist ma kerf, naddatki, kierunek sloja i nesting. Nie udawac, ze to program do rozkroju.
- Eksport CSV cytuje pola w cudzyslowie, zeby nazwa czesci z przecinkiem nie rozwalila kolumn.

## Kiedy sięgać po Claude, a kiedy pisać samodzielnie

- **Sięgnąć po Claude:** nowy typ czesci, inny format eksportu (XLSX, PDF), podglad rozkroju na plycie.
- **Zrobić samodzielnie:** reguly BOM i zalozenia produkcyjne. To one decyduja, czy lista nadaje sie do fabryki, a to wiedza o wyrobie, nie o kodzie.
