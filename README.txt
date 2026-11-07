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

Walka z bossami (poziom 10 każdej rundy; po pokonaniu bossa zaczyna się kolejna runda, po 4. — ekran "Gratulacje!"):
  Pasek życia: gracz ma pasek (100) i kilka żyć — trafienie zabiera część paska, po wyczerpaniu tracisz życie. Boss też ma pasek życia.
  R1 Admirał: rdzeń opancerzony (20% obrażeń), póki żyją dwa działa na skrzydłach -> najpierw zniszcz działa.
  R2 Gunship Alfa: czerwony pas ostrzega przed szarżą -> zjedź w bok; po szarży jest przegrzany (x2 obrażeń).
  R3 Lodowy Lewiatan: pancerz na zmianę zamknięty (nietykalny) i otwarty (cyjan) -> strzelaj tylko, gdy otwarty; pociski lodu spowalniają.
  R4 Cytadela: 4 generatory osłaniają rdzeń (im mniej ich, tym więcej obrażeń przyjmuje); po zniszczeniu wszystkich — obrotowy laser.
Poziomy trudności (menu, strzałki góra/dół): łatwy / średni / trudny zmieniają liczbę żyć, HP i szybkostrzelność wrogów, obrażenia,
częstość bonusów, okna na bossach i mnożnik punktów. Rekordy są osobne dla każdego poziomu.
