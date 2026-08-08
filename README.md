# 🎯 Nočná misia: Salzburg — bachelor party quest hra

Webová hra pre ženícha na jednu noc v Salzburgu. 10 misií, 100 bodov, porota a archív spomienok — všetko v jednej HTML stránke, bez servera, funguje priamo v mobile.

## Ako to funguje

- **Misie** — ženích vidí 10 úloh, každá za 10 bodov. Odklikáva si podúlohy (napr. policajt/hasič/zdravotník), počítadlá (kameň–papier–nožnice, psy), pridáva fotky a poznámky. Keď splní podmienky, stlačí **Splnené ✔**.
- **Porota** — partia si na tom istom telefóne (alebo cez zálohu na inom) otvorí záložku **Porota**, zadá PIN a splnené misie **overí pečiatkou** alebo zamietne.
- **Spomienky** — archív celej noci: fotky, zapísané hlášky a rady, časy splnenia, dosiahnutá hodnosť (Zelenáč → … → **Legenda Salzburgu** 🏆).

Dáta sa ukladajú lokálne v prehliadači (localStorage + IndexedDB), takže hra funguje aj bez internetu počas noci. Fotky sa automaticky komprimujú.

## Nastavenie pred akciou

1. Otvorte `index.html` a zmeňte PIN poroty (predvolený je `1234`):
   ```js
   const CREW_PIN = '1234';
   ```
2. Pri prvom otvorení stránka vypýta meno ženícha a nevesty (meno nevesty sa použije v misii č. 7). Mená sa dajú neskôr zmeniť v záložke Porota.

## Nasadenie (GitHub Pages)

Repo → **Settings → Pages → Deploy from a branch**, vyberte vetvu a `/ (root)`. Stránka bude na `https://<user>.github.io/<repo>/`. Potom stačí poslať ženíchovi link.

## Tipy

- Hru hrajte na **jednom telefóne** (ideálne ženíchovom) — všetky dáta žijú v tom prehliadači. Porota sa prihlási PIN-om na tom istom zariadení.
- Po skončení noci si v záložke Porota stiahnite **zálohu (JSON s fotkami)** — je to kompletný archív spomienok, dá sa neskôr načítať späť na hocijakom zariadení s touto stránkou.
- **Nepoužívajte anonymný/inkognito režim** — dáta by sa po zavretí zmazali.

## Misie

1. 🚨 Záchranné zložky — fotka s policajtom, hasičom a zdravotníkom
2. 💍 Rada od skúsených — pár spolu 30+ rokov + rada do manželstva
3. ✂️ Kameň – papier – nožnice — 5 súbojov s cudzími, aspoň 3 výhry
4. 👏 Standing ovation — celý podnik zatlieska, bez vysvetlenia
5. 🤫 Tichá objednávka — drinky výhradne pantomímou
6. 🤝 Starí kamoši — spoločná fotka s cudzou partiou
7. 👰 Menovkyňa nevesty — osoba s menom nevesty + fotka
8. 🐕 Psia smečka — fotky s 10 rôznymi psami
9. 🍺 Trofej z baru — podpivník s podpisom barmana
10. 🎨 Umelec noci — portrét na vreckovke ako dar
