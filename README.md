# DalMaps

Mobilna apka do nawigacji pieszej po hotelu Dalmahoy (Edynburg), oparta na
schematach stref ppoż. Jeden plik HTML (`index.html`), bez frameworków
i build stepu, UI po polsku, mobile-first.

## Deploy

Publikacja przez GitHub Pages — workflow `.github/workflows/pages.yml`
wdraża zawartość repo po każdym pushu. HTTPS jest wymagany, żeby na
iPhonie działało `DeviceMotionEvent.requestPermission()` (krokomierz).

Jeśli pierwszy deploy zgłosi, że Pages nie jest włączone: w ustawieniach
repo → Pages → Source ustaw **GitHub Actions** i uruchom workflow ponownie.
