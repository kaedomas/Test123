# Nočná misia: Salzburg — bachelor party quest hra

Webová hra pre ženícha na jednu noc v Salzburgu. 10 misií, 100 bodov, porota a archív spomienok — jedna HTML stránka, funguje v mobile aj offline.

**Živá stránka:** https://kaedomas.github.io/Test123/

## Ako to funguje

- **Misie** — ženích vidí 10 úloh po 10 bodov. Odklikáva podúlohy (policajt/hasič/zdravotník), počítadlá (kameň–papier–nožnice, psy), pridáva fotky a poznámky, a keď splní podmienky, stlačí **Splnené**.
- **Porota** — partia splnené misie **overí** alebo zamietne. Bez pečiatky poroty to nie je oficiálne.
- **Spomienky** — archív celej noci: fotky, hlášky, časy splnenia a hodnosť (Zelenáč → … → **Legenda Salzburgu**).

## Zdieľaná hra (každý na svojom telefóne)

Hra sa dá hrať na jednom telefóne (porota sa prihlási PIN-om, predvolene `1234`), alebo **zdieľane cez Supabase** — vtedy sa všetky telefóny synchronizujú.

### 1. Priprav Supabase (raz, ~3 minúty, free)

1. Na [supabase.com](https://supabase.com) si vytvor free projekt.
2. V **SQL Editore** spusti:
   ```sql
   create table if not exists public.games (
     id text primary key,
     data jsonb not null,
     updated_at timestamptz not null default now()
   );
   alter table public.games enable row level security;
   create policy "anon read"   on public.games for select using (true);
   create policy "anon insert" on public.games for insert with check (true);
   create policy "anon update" on public.games for update using (true);
   ```
3. V **Settings → API** si nájdi **Project URL** a **anon public key**.

### 2. Inicializuj hru

Otvor stránku, vyplň názov hry, mená a Supabase URL + anon key, klikni **Vytvoriť hru a získať linky**. Dostaneš dva linky:

- **Link pre ženícha** — hrací pohľad: odklikáva misie, fotí, píše poznámky. Porotu nevidí.
- **Link pre porotu** — všetko navyše: overovanie misií, mená, linky, zálohy.

Všetka konfigurácia cestuje v linku — partia nič nenastavuje, len klikne. Stav sa synchronizuje každých ~8 sekúnd; keď vypadne net, každé zariadenie hrá ďalej lokálne a po pripojení sa dobehne.

Fotky sa medzi zariadeniami prenášajú zmenšené (480 px); plná kvalita (1400 px) ostáva na telefóne, kde vznikli — po akcii si z neho stiahnite zálohu.

## Poznámky

- Anon key je verejný klientský kľúč, v linku ani v zdrojáku nevadí. Nikdy tam nedávaj `service_role` key.
- Po akcii: **Porota → Stiahnuť zálohu (JSON s fotkami)** = kompletný archív spomienok, dá sa kedykoľvek načítať späť.
- Nepoužívajte inkognito režim — lokálne dáta by sa po zavretí zmazali.
- Nasadzuje sa automaticky: push do vetvy → workflow prepíše vetvu `gh-pages` → GitHub Pages.

## Misie

1. Záchranné zložky — fotka s policajtom, hasičom a zdravotníkom
2. Rada od skúsených — pár spolu 30+ rokov + rada do manželstva
3. Kameň – papier – nožnice — 5 súbojov s cudzími, aspoň 3 výhry
4. Standing ovation — celý podnik zatlieska, bez vysvetlenia
5. Tichá objednávka — drinky výhradne pantomímou
6. Starí kamoši — spoločná fotka s cudzou partiou
7. Menovkyňa nevesty — osoba s menom nevesty + fotka
8. Psia smečka — fotky s 10 rôznymi psami
9. Trofej z baru — podpivník s podpisom barmana
10. Umelec noci — portrét na vreckovke ako dar
