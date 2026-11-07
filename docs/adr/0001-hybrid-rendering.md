# ADR-0001 — hybrydowe renderowanie

Status: proposed.

Kontekst: jednolita scena 3D obejmująca cały kraj byłaby zbyt kosztowna w przeglądarce. Zależy nam także na czytelnym pixel arcie i możliwości zoom od skali kraju do ulicy.

Decyzja do benchmarku: MapLibre (geograficzny podkład i kafle) + Three.js (stylizowane modele 3D i kamera izometryczna), z fallbackiem uproszczonych kafli przy małej skali.

Weryfikacja: dwie alternatywy na tej samej geometrii, pomiar FPS, transferu i jakości na desktop/mobile. Bez benchmarku nie oznaczać decyzji jako accepted.
