# Architektura — proponowana, podlega benchmarkowi

## Frontend
TypeScript, React, MapLibre GL JS dla mapowych danych 2D, Three.js dla opcjonalnej sceny izometrycznej 3D, stylizowane meshe, pixel-art materiały i shader pixelation. Jeden store stanu zawiera TimeSelection oraz ViewportState.

## Backend i źródła
Python + GDAL / Rasterio / pyproj do importu i georeferencji; PostgreSQL/PostGIS do zapisu zweryfikowanych obiektów. PMTiles / statyczne kafle dla kraju, wersjonowane paczki geometrii dla miast. Nie wczytujemy całej Polski do WebGL.

## Przepływ
Źródło → rejestr licencji i metadanych → georeferencja → normalizacja geometryczna → walidacja czasowa → przegląd historyczny → publikowany pakiet → mapa / karta obiektu.

## Separacja
Dane geograficzne nie są zależne od grafiki; jeden obiekt może być ikoną, bryłą i sceną szczegółową. Przypisujemy do obiektów źródła, prawa i przedziały dat; nie przypisujemy współczesnemu modelowi historycznej poprawności przez sam fakt zgodności geometrii.

## Wydajność
LOD, kaflowanie i culling; wydajność w przeglądarce i na telefonie to kryterium wyboru silnika. Raportujemy FPS, P95 czasu klatki, transfer, użycie pamięci, rozmiar pojedynczej sceny.

## Operacje
Nie przechowuj sekretów w repo; nie uruchamiaj ciężkich GIS importów w GitHub Actions. Staging wyłącznie w izolowanym środowisku po akceptacji. Żaden deploy produkcyjny bez zgody właściciela.
