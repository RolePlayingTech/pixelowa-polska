# Pixelowa Polska — atlas historii w pikselach

> **Stan:** publiczny projekt dokumentacyjny (7 listopada 2026). Nie ma jeszcze uruchomionej aplikacji ani zweryfikowanych rekonstrukcji.

**Pixelowa Polska** to interaktywny, pikselowy atlas historyczny: jeden świat obejmujący współczesny obszar Polski i historyczne ziemie państw polskich, który można oglądać w wybranej dacie. Globalny pasek czasu zmienia widoczne miasta, drogi, zabudowę, granice i nazwy; użytkownik nie traci punktu obserwacji.

## Główna obietnica

1. **Jedna mapa, jeden czas:** wybór roku działa na wszystkie warstwy, a nie tylko na pojedyncze historyczne obrazy.
2. **Pixel art oparty na geografii:** rzeczywiste obrysy i modele renderowane jako spójny świat izometryczny/3D.
3. **Prawda przed efektem:** nieznane pozostaje nieznane; rekonstrukcja i hipoteza są widocznie oznaczone.
4. **Źródła pod ręką:** kliknięcie obiektu pokazuje chronologię, pochodzenie geometrii, wiarygodność i licencje.
5. **Od całego kraju do wybranej ulicy:** cała Polska ma pokrycie geograficzne, zaś szczegółowe rekonstrukcje powstają etapami.

## Zakres pierwszej wersji

- Warstwa współczesna dla całej Polski jako techniczna baza (nie oznacza kompletnego historycznego 3D).
- Jeden globalny pasek czasu, oś wydarzeń lokalnych i link do widoku `?date=...&lat=...&lon=...&zoom=...`.
- Jedna warstwa historycznej geografii na poziomie kraju (pilotaż XVI wieku albo II RP, w zależności od audytu licencji i jakości).
- Pilotaż **wybranego fragmentu Warszawy** w 1935, 1945 i czasach współczesnych; tylko obiekty z prawidłowo przypisanym źródłem.
- Karty źródeł, stopień pewności i jawne obszary bez danych.

Nie obiecujemy pełnej rekonstrukcji każdego budynku ani płynnej animacji nieznanych stanów pośrednich. Tryb uliczny oraz automatyczna animacja zmian są poza pierwszym MVP, ale architektura je przewiduje.

## Dokumentacja

| Plik | Cel |
|---|---|
| [docs/01-vision.md](docs/01-vision.md) | Wizja, odbiorcy i zasady |
| [docs/02-product-requirements.md](docs/02-product-requirements.md) | PRD i kryteria akceptacji |
| [docs/03-experience.md](docs/03-experience.md) | Mapa, suwak, porównania, widok uliczny |
| [docs/04-architecture.md](docs/04-architecture.md) | Architektura, import i renderowanie |
| [docs/05-historical-data.md](docs/05-historical-data.md) | Weryfikacja historii i model czasu |
| [docs/06-sources-and-licenses.md](docs/06-sources-and-licenses.md) | Rejestr źródeł i licencji |
| [docs/07-rendering-spike.md](docs/07-rendering-spike.md) | Eksperymenty z silnikiem pixel art |
| [docs/08-roadmap.md](docs/08-roadmap.md) | Etapy i bramki jakości |
| [docs/09-quality.md](docs/09-quality.md) | Testy i kryteria akceptacji |
| [docs/10-backlog.md](docs/10-backlog.md) | Issues gotowe do przeniesienia na GitHub |
| [docs/11-open-decisions.md](docs/11-open-decisions.md) | Pytania i decyzje do podjęcia |
| [docs/research/comparables.md](docs/research/comparables.md) | Analiza inspiracji i repozytoriów |
| [docs/adr/](docs/adr/) | Decyzje architektoniczne |
| [AGENTS.md](AGENTS.md) | Reguły pracy agentów AI |

## Repozytorium

Repozytorium: https://github.com/RolePlayingTech/pixelowa-polska. Jest publiczne, ale własny kod nie ma jeszcze wybranej licencji. Skany i warstwy obce mają osobne zasady wykorzystania.

## Start współpracy

- Nowe dane muszą posiadać metadane źródła, praw i poziomu pewności.
- Zmiany przechodzą przez PR; produkcja wymaga odrębnego zatwierdzenia właściciela.
- Nie kopiujemy kodu/grafik z Cracow Pixel Map lub Wrocław Pixel Map bez licencji/zgody.
- Baza źródeł i gotowe kafle nie są automatycznie częścią otwartego repozytorium.

## Licencjonowanie projektu

**Licencja własnego kodu pozostaje do decyzji właściciela (`TBD`).** Do czasu wybrania licencji brak pliku `LICENSE` nie oznacza zgody na ponowne użycie. Dane zewnętrzne zachowują własne licencje, a każda publikowana warstwa musi przejść audyt praw.

## Punkt wyjścia

- Pierwowzór: https://michalpietralik.pl/cracowpixelmap/
- Open-source pixel renderer: https://github.com/RayNCooper/iso-cities
- Atlas zmian granic: https://github.com/chronoatlas-org/chronoatlas
- Dane historyczne: https://www.openhistoricalmap.org/ i https://atlasfontium.pl/
- Dane 3D: https://www.geoportal.gov.pl/pl/dane/inne-dane/modele-3d-budynkow/

Pełne opisy i zastrzeżenia znajdują się w dokumentacji. To **projekt niezależny**, nie fork żadnej z wymienionych map.