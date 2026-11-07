# Historyczny model danych

## Najważniejsze rozróżnienia
- Obiekt mógł istnieć, ale nie mamy jego wyglądu.
- Brak danych nie oznacza, że obiektu nie było.
- Data wykonania zdjęcia/mapy nie jest automatycznie datą wzniesienia obiektu.
- Czas obserwacji, czas obowiązywania, data źródła i data importu są odrębne.
- Sprzeczne źródła mogą być prezentowane jako konkurencyjne interpretacje.

## Model
Feature (tożsamość obiektu) → State (wariant stanu w przedziale czasu) → Geometry (położenie i kształt) → Claims (twierdzenia) → Sources (archiwalne rekordy) → RightsReview. Obiekt z wieloma przebudowami ma wiele stanów.

Valid from jest włącznie, valid to wyłącznie; precyzja może być year, decade, century, range, unknown. Nie wymuszaj pozornej dokładności dat. Stany bez danych o geometrii mogą być ważne.

## Stopnie pewności
A — bezpośrednio udokumentowane; B — mocno uprawdopodobnione; C — hipoteza; D — nieznane. Osobno oceniaj istnienie, pozycję, kształt, fasadę i datowanie. Stopnia A nie nadaje automat bez recenzji.

## Kontrole
Każda publikowana hipoteza wymaga statusu rights_review=approved i odnośników do źródeł. Syntetyczne rekordy są trwale oznaczone i nigdy nie trafiają do oficjalnej rekonstrukcji. Testuj daty graniczne oraz brak danych.
