# florbal.app – stav projektu

## Co je hotovo
Pět HTML souborů nasazených na Cloudflare Pages:
- `index.html` — homepage s hero fotkou (míček), dvěma dlaždicemi (Turnaje v Čechách → `seznam.html?region=cr`, Zahraničí → `seznam.html?region=zahranici`), filtrovací lištou a přehledem nejbližších turnajů
- `kalendar.html` — měsíční kalendář s barevnými tečkami podle kategorie (muži/ženy/starší mládež/mladší mládež), filtry, detail panel jako centrované modální okno s míčkem na pozadí
- `seznam.html` — řádkový seznam turnajů seskupený po měsících, vyhledávání, filtry (Uvnitř/Venku, Kategorie, Kraj + skupinové volby ČR/Zahraničí, přepínání měsíců), detail panel
- `pridat.html` — formulář pro přidání turnaje (název, popis, datum od/do, město, kraj, prostředí, formát jako checkboxy, kategorie jako multiselect s Jiné, startovné + měna, web, email)
- `contact.html` — kontaktní formulář (email + zpráva), odesílá na cechjan@seznam.cz

## Design
- Barvy: červená `#D62B2B`, černá, bílá
- Fonty: Barlow Condensed (nadpisy), Barlow (text)
- Material Symbols Outlined ikony
- Fixed černý header s červenou linkou dole, výška 54px
- Hero fotka: `hero.jpg` (fialový florbalový míček)
- Dekorativní míček `tab.png` v detailních kartách (30% průhlednost)
- Favicon: `tab.png`

## Soubory na GitHubu / Cloudflare
```
index.html
kalendar.html
seznam.html
pridat.html
contact.html
hero.jpg
tab.png
sitemap.xml
robots.txt
```

## Kategorie
**Muži:** Muži (U23+), U23, U19 / Junioři, U17 / Dorostenci, U15 / Starší žáci, U13 / Mladší žáci, U11 / Elévové, Přípravka, Mini přípravka, Veteráni

**Ženy:** Ženy (G23+), G23, G19 / Juniorky, G17 / Dorostenky, G15 / Starší žákyně, G13 / Mladší žákyně, G11 / Elévky, Přípravka (dívky), Mini přípravka (dívky), Veteránky

**Ostatní:** Smíšené, Jiné (volný text)

## Barvy kategorií (badges + tečky v kalendáři)
- 🔴 červená = Muži (U23+), U23, Veteráni
- 🔵 modrá = Ženy (G23+), G23, Veteránky
- 🟢 zelená = starší mládež (U19/U17, G19/G17)
- 🟠 oranžová = mladší mládež (U15 a níž)
- 🟢 zelená = Smíšené

## Formáty
5+1, 3+1 (checkboxy — lze vybrat obojí)

## Kraje v dropdownu
**ČR:** Praha, Středočeský, Jihočeský, Plzeňský, Karlovarský, Ústecký, Liberecký, Královéhradecký, Pardubický, Vysočina, Jihomoravský, Olomoucký, Zlínský, Moravskoslezský

**Zahraničí:** Slovensko, Ostatní zahraničí

## Google Sheets
- Složka: **Florbal** v Google Drive (účet dumazahrada@gmail.com)
- Sheet: **Turnaje – přihlášky**
- ID: `11cd32XxW3rZOwQIx1BOk2klU_Ww9IzsIiupEJeM9V78`
- **CSV URL:** `https://docs.google.com/spreadsheets/d/e/2PACX-1vQW8jApm0jDnBw2NoJS0VsReF7sIRcrDHuw7nLsaX9wziVi6dL4gutYFUa3jiziEcPz2Jc5yMWjQkj-/pub?gid=0&single=true&output=csv`
- Sloupce A–N: Časové razítko, Název, Popis, Datum od, Datum do, Město, Kraj, Prostředí, Formát, Kategorie, Startovné, Web, Email, Schváleno
- Schválení: ručně napsat **ANO** do sloupce N

## Apps Script
- URL: `https://script.google.com/macros/s/AKfycbyIZBQMAq1pOWR6UyFt0570b45U0PAJDDgiEP497TOuNvnWUm81DpqtN-cBrBl5IONwug/exec`
- Zpracovává: přidání turnaje (zapíše do Sheets + notifikace) + kontaktní zprávy (`typ: 'kontakt'`)
- Notifikace na: `cechjan@seznam.cz`
- Potvrzení pořadateli: na email zadaný ve formuláři
- Po každé změně kódu nutno nasadit novou verzi: Nasadit → Spravovat nasazení → tužka → Nová verze

## Hosting
- **Cloudflare Pages** — zdarma, napojeno na GitHub repozitář `JanCechMaximus/florbal-app`
- **Doména:** `florbal.app` (registrována přes Cloudflare)
- GitHub repozitář: `https://github.com/JanCechMaximus/florbal-app`
- Live URL: `https://florbal.app`

## SEO
- Meta description na všech stránkách
- Open Graph tagy (og:title, og:description, og:image, og:url)
- `sitemap.xml` nahraný na web
- `robots.txt` s povoleným přístupem pro Googlebot, facebookexternalhit, Twitterbot
- Google Search Console: ověřit přes DNS TXT záznam v Cloudflare

## Technické poznámky
- Žádný framework, čisté HTML/CSS/JS
- Data flow: formulář → Apps Script → Google Sheets → web čte CSV
- CSV parser podporuje víceřádkové hodnoty v uvozovkách (dlouhé popisy)
- `mode: 'cors'` u fetch na CSV URL
- Zobrazují se jen turnaje kde sloupec N = ANO (case-insensitive)
- Datum musí být ve formátu `YYYY-MM-DD` (ne `1.5.2026`)

## Známé věci k dodělání / nápady
- Sdílené detail.js — detail karta je implementována zvlášť v kalendáři i seznamu, ideálně sjednotit
- Hero fotka — nyní fialový míček, lze vyměnit za akční florbalovou fotku
- Filtry na homepage filtrují jen 5 zobrazených turnajů, ne všechny
