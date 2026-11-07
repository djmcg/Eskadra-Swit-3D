Eskadra Świt 3D (Three.js / WebGL)

Wgraj cały folder na serwer (index.html + models/ + img/). Gra używa modułów ES i plików .glb,
więc nie działa po otwarciu z dysku (file://) - potrzebny jest serwer HTTP, np. lokalnie:
    python -m http.server 8000     ->  http://localhost:8000/
Three.js ładuje się z CDN (jsdelivr, wersja 0.160.0), czcionki z Google Fonts.

Modele: models/*.glb eksportowane z Blendera (skrypt ../eksport_glb.py + ../fighters_lowpoly.py, ../srodowisko_lowpoly.py).
