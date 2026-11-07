Eskadra Świt 3D (Three.js / WebGL)

Wgraj cały folder na serwer (index.html + models/ + img/). Gra używa modułów ES i plików .glb,
więc nie działa po otwarciu z dysku (file://) - potrzebny jest serwer HTTP, np. lokalnie:
    python -m http.server 8000     ->  http://localhost:8000/
Three.js ładuje się z CDN (jsdelivr, wersja 0.160.0), czcionki z Google Fonts.

Modele: models/*.glb eksportowane z Blendera (skrypt ../eksport_glb.py + ../fighters_lowpoly.py, ../srodowisko_lowpoly.py).

Rozgrywka: 4 rundy po 10 poziomów (poziom 10 = boss). Rundy: 1 Morze, 2 Pustynia, 3 Zima, 4 Twierdza na lawie
(w rundzie 4 tylko wieże naziemne). Nowi wrogowie: kamikadze (R1), śmigłowiec bojowy (R2), lodowy snajper (R3), wieże (R4).
Bonusy są rzadkie (odstęp 12 s, maks. 3 na poziom), 1UP tylko za bossa, limit 5 żyć. Wróg, który przeleci dołem, to "przeciek":
5 przecieków w poziomie = utrata życia (nie dotyczy rundy 4).
Testy logiki (Playwright): hooki window.__eskadra.symuluj / skocz / info.
