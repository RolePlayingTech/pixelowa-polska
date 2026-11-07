# Plan wykonawczy v1 — Pixelowa Polska: od małego wycinka do atlasu kraju

Status: **rekomendacja do przekazania agentowi**, nie zatwierdzenie publikacji danych ani produkcyjnego wdrożenia. Data przeglądu: 2026-11-07. Niniejszy dokument uszczegóławia README, PRD oraz issues PP-001–PP-007; nie zastępuje przeglądu praw i testów silnika.

## 1. Cel i granice odpowiedzialności

Produkt docelowy: jedna interaktywna, izometryczna/pikselowa mapa Polski z globalnym wyborem daty. Przybliżenie w miastach pokazuje historycznie uzasadnione bryły budynków, a wybrane obiekty mają karty dowodowe. Dane są niezależne od renderera. **Nie obiecujemy całej Polski szczegółowo zrekonstruowanej w każdym roku.**

W pierwszym wydaniu udowadniamy:
- pikselową jakość obrazu (nie sam filtr CSS);
- stabilną kamerę podczas zmiany czasu;
- co najmniej dwie *udokumentowane* postacie konkretnego miejsca, plus stan braku danych;
- trwałe identyfikatory obiektów i źródeł, odtwarzalne linki do mapy;
- tani pipeline tworzenia kolejnych historycznych wycinków;
- brak nielegalnych kopii map/zdjęć i brak zmyślonych danych historycznych.

## 2. Proponowany wycinek pilotażowy — Oś Saska w Warszawie

**Kandydat główny: zachodnia pierzeja placu Piłsudskiego, zwłaszcza Pałac Saski i Grób Nieznanego Żołnierza, z niewielkim fragmentem dojścia od Ogrodu Saskiego.** Granicę poligonu i bounding box trzeba wyznaczyć z geodanych dopiero w ramach audytu. Rozmiar docelowy: mały obszar rzędu kilkuset metrów, a nie cała dzielnica.

Dlaczego: na niewielkiej scenie można porównać monumentalny przedwojenny pałac, zburzony obiekt i zachowany pomnik oraz współczesne otoczenie. Istnieją niezależne źródła: materiały Pałac Saski, Archiwum BOS, miejski Portal Historyczny Warszawy z fotoplanem 1935 i planem zniszczeń 1945–1946, oraz GUGiK LoD1 dla współczesnego punktu odniesienia. Główne odnośniki:
- https://warszawa.ap.gov.pl/wystawy-o-biurze-odbudowy-stolicy/
- https://archiwa.gov.pl/cyfrowy-plan-inwentaryzacji-zniszczen-warszawy-biura-odbudowy-stolicy-z-lat-1945-1946-dostepny-online/
- https://mapa.um.warszawa.pl/portal-historyczny/
- https://palacsaski.pl/historia/palac-saski-rezydencja-krolewska
- https://palacsaski.pl/historia/grob-nieznanego-zolnierza-pamiec-o-poleglych-wiecznie-zywa
- https://www.geoportal.gov.pl/pl/dane/inne-dane/modele-3d-budynkow/

**Trzy ujęcia do sprawdzenia:** ok. 1935 (przedwojenny pałac), 1945 (udokumentowane zniszczenie; nie tworzyć fikcyjnego rozkładu gruzu), oraz punkt odniesienia **2024** z etykietą daty i pochodzenia geodanych. Nie oznaczać 2024 jako bezwarunkowo aktualnego stanu 2026: w 2026 r. na tym terenie prowadzone są prace archeologiczne i geologiczne. Konkretny dzień/rok stanu i zakres budynków mogą ulec korekcie po audycie.

Minimalny pierwszy widok: **Pałac Saski + arkady Grobu Nieznanego Żołnierza + zarys placu**. Rozbudowa o Pałac Brühla i kamienice Królewskiej jest osobnym zadaniem, dopiero gdy dane są wystarczające. Nie kopiować istniejących modeli 3D Pałacu Saskiego.

Wariant zapasowy, jeśli licencje, geometria albo źródła zablokują pilotaż: mały fragment placu Zamkowego, z osobnym testem dostępności archiwaliów; nie rozszerzać obszaru automatycznie. Uzasadnienie wyboru, tabela źródeł, niepewność oraz prawa muszą być w PR.

## 3. Prawa i jakość dowodów: bramka bez wyjątków

- Informacje z oglądanych stron internetowych służą do identyfikacji materiałów, ale **możliwość oglądania nie jest prawem do wykorzystania**.
- GUGiK publikuje modele 3D budynków do bezpłatnego wykorzystania; trzeba zachować proweniencję i atrybucję odpowiednią dla wybranej warstwy.
- Szukaj w Archiwach dopuszcza ponowne wykorzystanie wielu kopii, ale zależy to od oznaczeń konkretnego obiektu (domena publiczna, prawa archiwum, ograniczone lub nieustalone). Sprawdzić każdy skan.
- Warszawa1939.pl oznacza materiały jako CC BY-NC: nie używać ich swobodnie w ewentualnej komercyjnej dystrybucji ani jako nieweryfikowanego źródła kopiowanej geometrii.
- Warunki fotoplanów oraz zasobów miejskiego Portalu Historycznego sprawdzić **dla konkretnych usług i warstw**, nie domniemywać dowolnej licencji na podstawie dostępu do portalu.
- OpenHistoricalMap: zwykle CC0, jednak niektóre rekordy mają własne tagi license i osobne obowiązki; OSM to ODbL. Nie mieszać zbiorów bez przeglądu skutków licencyjnych.
- Do publicznego repo: wyłącznie kod, własne lub dopuszczone prawnie dane i metadane. Materiały zablokowane: link + opis, bez kopii assetu.

Każdy element rekonstrukcji ma posiadać w systemie: stabilny ID, zakres czasu i precyzję, geometrię albo jawny jej brak, źródła z sygnaturami lub jednoznacznymi URL, poziomy pewności osobno dla istnienia, położenia, bryły, wysokości i detalu, opis interpretacji oraz status uprawnień do publikacji. Stopień A nie jest przyznawany automatycznie przez AI.

## 4. Technika: decyzja po porównaniu, nie przed

**Dwa równoległe, ograniczone eksperymenty na tej samej syntetycznej scenie:**
A. MapLibre ze stylizowanymi bryłami/extrusions plus lekkie efekty.
B. MapLibre + osobna warstwa Three.js/scene z kamerą zbliżoną do izometrycznej, stylizowanymi modelami i renderowaniem low-resolution/nearest-neighbor.

Przy małej skali kraju dopuszczalne uproszczone kafle 2D/PMTiles. Nie zakładać, że jeden renderer przybliży cały kraj do ulicy bez problemów. Testować spójność pozycji geograficznej 3D i mapy, obrót, hit testing, zmianę czasu, etykiety na hi-res UI i mobile.

**Pixel art** to język form i materiałów: geometrycznie czytelne dachy, drzewa i teren, kontrolowana paleta, sylwetki i cienie, stała reguła skali piksela. Sam filtr pixelate na standardowym basemapie nie wystarcza. Model nie może sugerować szczegółów historycznych, których nie da się uzasadnić.

## 5. Strumienie pracy i właściciel odpowiedzialności

Jeden silny agent-integrator odpowiada za kontrakty API, decyzje ADR, integrację i przygotowanie PR. Deleguje maksymalnie 3–4 rzeczywiście niezależne zadania naraz:
1. **Sources/History/Rights:** poligon, katalog obiektów i źródeł, licencje, matryca pewności, raport luk.
2. **Renderer/Geo:** dwie demonstracje, benchmarky i rekomendowany kontrakt kamery; wariant fallback.
3. **Product/UX/Pixel art:** oś czasu, ekran, paleta, poziomy zoom i prototyp porównań, dostępność.
4. **Data/Pipeline:** model stanu historycznego, walidatory, importer, fixture testowe, provenance.
Niezależne QA/review dopiero po wynikach każdego strumienia, bez uznawania auto-review autora za niezależny audyt.

Kontrakty integracyjne wymagane przed równoległym kodowaniem:
- ViewState: lat/lon/zoom/bearing/pitch oraz wybrany obiekt.
- TimeSelection: data/przedział/precyzja i status dostępności dla danego obszaru.
- HistoricalFeature + FeatureState + EvidenceClaim + Source + RightsDecision; osobny katalog Coverage dla miejsca/epoki/rodzaju danych.
- RenderFeature API przyjmujący obiekty i stan widoczności, NIE łączący danych źródłowych z shaderem.
- URL/deeplink oraz jawna polityka danych cache i wersjonowania.

## 6. Kolejność — sześć etapów z bramkami

### G0. Uzgodnić kontrakty i pilotaż
Wejście: aktualne README, AGENTS, PP-001–007. Wynik: potwierdzony mały poligon, macierz epok, zakres assetów i uprawnień, mock UX, budżety wydajności. **Stop** jeśli brak drogi do choć dwóch różnych, źródłowo uzasadnionych stanów.

### G1. Techniczne proof of concept na danych FIKCYJNYCH
Na syntetycznej geometrii zrobić dwa rendery, jeden pikselowy styl, pan/zoom/rotate, wybór 3 dat, brak ruchu kamery po zmianie daty, brak danych jako jawny stan. Wynik: screenshoty/wideo, FPS i pamięć, ADR wyboru silnika. Testować bez ryzyk praw do archiwaliów.

### G2. Historyczny data pack
Opracować 10–30 wybranych obiektów/fragmentów, tylko tyle, ile można uzasadnić: minimum obrys i stan istnienia. Dla wybranych 1–3 landmarków detale bryły. Powtarzalna georeferencja z punktami kontrolnymi, residual error i raportem; źródła oraz prawa przy każdej jednostce. Nie naśladować szczegółów nieudokumentowanych fasad.

### G3. Działający pilot 1935 / 1945 / 2024
Pikselowa scena Pałacu Saskiego + Grobu Nieznanego Żołnierza, przybliżanie i rotacja, 3 udokumentowane punkty czasu (w 1945 bez fikcyjnego gruzowiska), karty źródeł, niepewność, komunikaty o lukach, deeplink. Najpierw dwa dobrze udokumentowane stany, trzeci gdy źródła pozwolą. Testy na desktop i telefonie.

### G4. Ogólnopolska mapa i interoperacyjność
Geograficzna nawigacja dla całej współczesnej Polski, typy warstw, pokrycie historyczne, skok z kraju do pilota. Jedna historyczna warstwa kraju w dopuszczonej licencji (z zasięgiem odpowiadającym faktycznym źródłom). Dwa niezależne tryby geografii: współczesne granice Polski versus historyczny zasięg państw/polskich ziem. Braki historyczne oznaczane, NIE maskowane współczesnymi budynkami jako dawne.

### G5. Stabilizacja i odbiór właściciela
Budżety transferu, testy temporalne, źródła/prawa, mobile, dostępność, wydajność, porównanie wyników z wymaganiami, lista otwartych błędów, krótki film demonstracyjny. Staging wyłącznie po świadomej akceptacji infrastruktury. **Produkcja, merge strategiczny i rozbudowa w wielu miastach wyłącznie po zatwierdzeniu przez właściciela.**

## 7. Scenariusze akceptacyjne (manualne + automatyczne)

- Ta sama kamera, ten sam ID obiektu i jedna lokalizacja: 1935 -> 1945 -> 2024. Zmienia się tylko czas i dane, nie położenie użytkownika.
- Rok przed pierwszym wiarygodnym źródłem: **„brak potwierdzonej rekonstrukcji”**, nie fałszywa pustka ani przeniesiony wstecz dzisiejszy budynek.
- Źródło bez prawa do publikacji: rekord nie wchodzi do publicznej paczki, nawet jeśli historycznie jest trafny.
- Po stronie źródła rozdzielone są „nie istniał”, „zniszczony”, „brak wiedzy”, „przetrwał, nie znamy wyglądu”; nie wolno domyślnie renderować dowolnej z tych kategorii jako innej.
- Rozbieżne daty lub geometrie: raport konfliktu i brak automatycznej promocji pewności.
- Frontend działa na standardowym laptopie i telefonie klasy średniej. Założenia docelowe do zmierzenia: płynność co najmniej ok. 30 FPS na telefonie w pilotażu; czas zmiany epoki w cache ok. 1 s; brak krytycznych błędów i czytelne etykiety. Raport musi zawierać urządzenie, sieć, obszar i metodę testu.
- Brak ciężkich zadań GitHub Actions; testy lokalne/izolowany runner, importy offline. Żadnych sekretów w logach/commicie.
- Demonstracja przechodzi bez ręcznych sztuczek i bez obowiązkowej rejestracji użytkownika.

## 8. Czego na razie świadomie NIE robimy

Nie budujemy pełnego Street View, tłumów i interaktywnych postaci, rekonstrukcji fasad każdego polskiego domu, AI-upiększania historycznych zdjęć jako faktów, gry survivalowej, globalnej płynnej animacji pomiędzy nieudokumentowanymi datami, encyklopedii wszystkich wydarzeń ani panelu społecznościowego. To prace po G5.

## 9. GitHub i zasady autonomii

- Zaczynać od issue PP-001/002/003/004/005/006/007 i tego planu. Nie mnożyć issues bez potrzeby.
- Każdy większy strumień w osobnym branchu i PR. PR zawiera: co zmieniono, screenshot/demo, dane/sources, licencje, testy, limity, ryzyka i powiązane issue.
- Na początku fazy raportować decyzje, na końcu raport i odtwarzalne polecenia. Bez automatycznego deployu produkcyjnego. Pozwolenie na tworzenie PR nie jest pozwoleniem na produkcyjne wdrożenie.
- Przerwać i eskalować: brak prawa do kluczowego materiału, brak dwóch wiarygodnych stanów, niestabilny renderer na telefonie, niekontrolowany koszt, nieznana baza danych, historyczna sprzeczność wymuszająca fikcję.

## 10. Pierwsze zlecenie dla agenta

W **jednej delegacji** poleć integratorowi wykonanie G0–G5 jako serię małych, weryfikowalnych PR. Agent zaczyna od G0 + G1, równolegle przygotowuje kwerendę historyczno-prawną G2; po pozytywnym wyniku bramki G1 może samodzielnie przejść do G2/G3, zgodnie z udokumentowanym ADR i niezależnym review. Nie powinien zatrzymywać się po samym napisaniu planu ani czekać na nowe prompty po każdym małym kroku. Ma dostarczyć działające MVP z demem i raportem, nie tylko dokumentację.

**Automatyczne przejście przez bramkę** jest dozwolone tylko po spełnieniu sprawdzalnych kryteriów (testy, źródła, licencje, wyniki wydajności, demonstracja). Jeśli brak źródeł lub praw do konkretnego stanu, agent ma ograniczyć zakres i jawnie oznaczyć lukę, a nie sfabrykować treść. Musi zatrzymać się przed wydatkami, dostępem do nowych tajnych systemów, produkcyjnym wdrożeniem lub zewnętrzną publikacją wymagającą zgody właściciela. W razie zasadniczego nierozstrzygniętego konfliktu architektonicznego przedstawić decyzję z rekomendacją do zatwierdzenia.

Najpierw mała scena, później ogólnopolski szkielet — to **jeden projekt**, a nie dwa niezależne produkty. Pełne historyczne 3D całej Polski pozostaje programem wieloletnim, nie warunkiem zamknięcia pierwszej delegacji.
