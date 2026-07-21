# DalMaps

Mobilna apka (PWA) do nawigacji pieszej po hotelu Dalmahoy (Edynburg),
oparta na schematach stref ppoż. Jeden plik `index.html` (bez frameworków
i build stepu, UI po polsku, mobile-first) + `manifest.webmanifest`,
`sw.js` i ikony.

**Uwaga:** geometria pięter w SVG jest na razie schematyczna — kody stref
Z01–Z41, przypisanie stref do pięter i kolory skrzydeł trzeba skalibrować
z fizycznym planem ppoż. hotelu. Cała geometria i konfiguracja skrzydeł
siedzi w jednym miejscu (`WINGS` + inline SVG w `index.html`), więc
podmiana nie zmienia logiki.

## Funkcje

- Piętra (parter/1/2/3) jako inline SVG, `viewBox 0 0 100 114`.
- Trasy: obiekt tras budowany z kroków `S(floor, overlays, marks, text,
  wingPick, len)`; przerywana czerwona ścieżka na planie.
- Krokomierz: `devicemotion`, filtr LP grawitacji, próg 1,4 m/s²,
  refrakcja 320 ms, krok domyślnie 0,75 m; kropka sunie po ścieżce przez
  `getPointAtLength`. Na iOS wymaga HTTPS i zgody z gestu użytkownika.
- PWA: manifest + service worker cache-first — działa offline po
  pierwszym otwarciu, instaluje się na ekranie głównym.
- Screen Wake Lock, gdy krokomierz aktywny (z komunikatem, gdy brak API).
- `localStorage`: przypięte skrzydło pokoju 136, długość kroku,
  ostatnia trasa start/cel.
- Po przypięciu skrzydła trasa na 1. piętrze prowadzi krótszym łukiem
  pętli od klatki Z01–Z02, zamiast podświetlać całą pętlę.

## Deploy

Workflow `.github/workflows/pages.yml` po każdym pushu wypycha zawartość
repo na gałąź `gh-pages`, z której serwuje GitHub Pages:
`https://onlinekot.github.io/DalMaps/`. HTTPS jest wymagany, żeby na
iPhonie działało `DeviceMotionEvent.requestPermission()` (krokomierz).
