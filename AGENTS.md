# AGENTS.md — reguły dla agentów AI

## Misja

Budujemy niezależny, pikselowy atlas historii Polski. **Wierność historyczna, legalność danych, wydajność i utrzymanie** mają pierwszeństwo przed ilością wygenerowanego kodu. Rozpocznij od README i dokumentów `docs/`.

## Niezmienniki

1. Żaden obiekt nie może być opisany jako historycznie udokumentowany bez odniesienia do źródła, zakresu dat, typu dowodu i informacji o prawach.
2. Odróżniaj: *obiekt nie istniał*, *brak dowodów*, *istnienie niepewne*, *stan zrekonstruowany*. Nie renderuj nieznanego jako pewnego.
3. `observed_at`, `valid_time`, `source_date`, `ingested_at` to różne pojęcia. Wątpliwa data musi mieć precyzję i niepewność.
4. Granice: kontrola administracyjna, roszczenia i uznanie prawne to różne relacje; nie ujednolicaj ich na siłę.
5. Nie używaj współczesnych obrysów jako dowodu dawnej geometrii bez źródeł.
6. Nie używaj generatywnej grafiki jako dowodu historycznego. Hipotezy graficzne muszą być oznaczone.
7. Nie pobieraj hurtowo z publicznych Overpass/API/archiwów bez polityki rate-limit i zgody tam, gdzie potrzebna.
8. Nie kopiuj zastrzeżonych materiałów lub kodu innych map. Sprawdzaj **licencję dokładnego pliku lub modułu**, nie tylko repozytorium.
9. Nie publikuj skanów, fotografii, danych ani modeli bez przejścia bramki praw (źródło, licencja, atrybucja, komercyjne użycie, prawa do modyfikacji, obowiązki przy redystrybucji).
10. Żadne wdrożenie produkcyjne bez jednoznacznej zgody właściciela.

## Organizacja pracy

- Osobne zadania: pozyskanie źródeł, georeferencja, model danych, renderowanie, UX, QA/licencje.
- Prace równoległe tylko w izolowanych branchach/PR; konflikty rozstrzyga integrator.
- Minimalny niezbędny CI: testy schematów, walidacja metadanych, smoke renderowania; kosztowne importy offline.
- Każdy PR zawiera: zakres, kryteria odbioru, źródła, ryzyka, testy i screenshot przy zmianach UI.
- Nie wykonuj deployu do produkcji; środowisko testowe dopiero po ustaleniu infrastruktury i akceptacji.
- Nie zakładaj, że istnieje aplikacja, tajne klucze, dostęp do Hetznera lub gotowa baza danych.

## Definition of Done

- Wykaz źródeł, licencji i atrybucji dla każdej nowej warstwy.
- Powtarzalny import i wersja zestawu danych.
- Testy roku przed/po granicy obowiązywania obiektu oraz braku danych.
- Wynik audytu wydajności dla docelowego poziomu zoom.
- Zaktualizowana dokumentacja i brak ukrytych hipotez.

## Zakazy

- Nie przypisuj stopnia A masowo na podstawie samego dopasowania AI.
- Nie dodawaj płatnych integracji ani ciężkiego CI bez uzasadnienia.
- Nie dopisuj nieistniejących źródeł, adresów URL, sygnatur archiwalnych ani szczegółów zabytków.
- Nie twórz fikcyjnej historii do widoku produkcyjnego.