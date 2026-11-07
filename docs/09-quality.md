# Jakość, testy i bramki

- Schemat JSON i syntetyczny fixture muszą przejść walidację.
- Testy daty przed istnieniem / w trakcie / po oraz niepewnej daty.
- Brak danych jest widoczny i nigdy nie renderuje się jako „puste historycznie”.
- Każdy obiekt oznaczony jako udokumentowany ma źródło i datowanie.
- Sprawdzenie praw autorskich w trybie fail-closed: brak zatwierdzenia blokuje publikację.
- Benchmark desktop/mobile: FPS, P95 renderu, pamięć, transfer.
- Testy deeplinków, klawiatury i dostępności.
- Tylko lekki CI; duże importy i render 3D poza płatnym GH Actions.
- CI i review nie zastępują decyzji właściciela o wdrożeniu produkcyjnym.
