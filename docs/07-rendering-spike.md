# Spike renderowania pixel art

## Cel
Porównać na identycznej geometrii co najmniej dwa warianty:
1. MapLibre + budynki w stylu pixel art, lekkie 3D.
2. MapLibre + Three.js + materiały stylizowane + pixelation postprocessing.

Dodatkowa kontrola: wstępnie wyrenderowane kafle przy odległym zoomie.

## Sceny testowe
Kraj (wiele obiektów na ekranie), regularna dzielnica, centrum ze skomplikowaną geometrią oraz syntetyczny fragment dwóch epok. Testy desktop / średni telefon.

## Metryki
P95 klatki, średni FPS, memoria GPU/JS, transfer danych, czas pierwszej interakcji, pixel-art readability w 3 skalach, czas zmiany daty i utrzymanie pozycji kamery. Używaj krótkich, powtarzalnych testów i nie uruchamiaj kosztownego CI.

## Akceptacja
Niezależny wynik pokazowy dla dwóch dat z zachowaną kamerą, raport z profili wydajności i ADR uzasadniający wybrany renderer. Syntetyczne dane oznaczone jako syntetyczne.
