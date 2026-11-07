---
name: cakes-by-anja
description: Ključni podatki za gradnjo in urejanje strani Cakes by Anja (statični generator v Pythonu, vsebina v Markdownu + HTML blokih, objava na GitHub Pages, mobilni prikaz). Uporabi pred vsakim dodajanjem ali urejanjem strani, menija, kontaktnih podatkov, slik, obrazca, videza ali generatorja v tem projektu.
---

# Cakes by Anja – kako graditi ta projekt

Spletna stran za domače torte. Jezik strani in dela z uporabnikom: **slovenščina**.
Večina obiskovalcev bo na **telefonu** – vsako spremembo preveri tudi pri širini 375 px.

## Zgradba

- `content/**/index.md` → vsaka mapa je ena stran. Strani: `/` (Domov), `/torte`, `/ponudba`,
  `/o-meni`, `/kontakt`. Vsaka `.md` **mora** imeti naslov `# ...` (sicer `no h1 header found`).
- `site.json` → `name`, `lang`, `description`, `tagline`, kontakt (`phone`, `phone_display`,
  `whatsapp`, `email`, `instagram`, `location`), `web3forms_key` in `nav`.
- `template.html` → oznake `{{ Title }}`, `{{ SiteName }}`, `{{ Lang }}`, `{{ Nav }}`, `{{ Content }}`
  in poljubne `{{ site.kljuc }}`. Vsebuje glavo (znamka, gumb »Naroči torto«, meni), nogo
  s kontaktom in spodnjo vrstico za telefon (Pokliči · WhatsApp · Naroči).
- `static/` → `index.css`, `favicon.svg`, `images/`; skopira se v izhodno mapo kot je.
- `src/` → generator in testi `test_*.py` (unittest).

## Generator – kaj zna

- `{{ site.kljuc }}` se zamenja v predlogi **in v vsebini** z (escapano) vrednostjo iz `site.json`.
  Neznan ključ → `ValueError: unknown site value`. Kontaktne podatke nikoli ne piši ročno v vsebino,
  vedno prek `{{ site.* }}`.
- Meni: trenutna stran dobi `aria-current="page"` (URL iz poti mape, npr. `/torte`).
- **HTML bloki:** blok, ki se začne z `<` + črka/`!`/`/`, gre na stran nespremenjen (`RawNode`).
  Znotraj HTML bloka **ni praznih vrstic** (prazna vrstica konča blok) in Markdown se ne obdela.
- Basepath: `render_page` zamenja `href="/` in `src="/`. Notranje povezave in slike vedno z `/`.
  Drugi atributi (npr. `action`, `content`) se ne popravljajo.

## Ukazi

- `./test.sh` – testi (vedno poženi po spremembi v `src/`).
- `./main.sh` – gradnja v `public/` + strežnik na http://localhost:8888.
- Predogled v brskalniku: `.claude/launch.json` konfiguracija `stran` (streže `public/`),
  pred tem `python3 src/main.py "/" ./public`.
- `./build.sh` – produkcijska gradnja v `docs/` (basepath `/Cakes_by_Anja/`).

## Markdown

- Podprto: naslovi, odstavki, `**krepko**`, `_ležeče_`, `` `koda` ``, kodni bloki, citati `>`,
  seznami `- ` in `1. `, povezave, slike.
- **Ni podprto:** tabele (cene piši kot seznam), `*ležeče*`, gnezdeni seznami.
- Neparni `**` ali `` ` `` → `invalid markdown: unmatched ...`.
- Slog: vikanje, topel in preprost ton.

## Gradniki (CSS razredi)

- `.btn`, `.btn-ghost`, `.btn-whatsapp`, `.btn-viber`; vrsta gumbov v `<p class="actions">`.
- `.hero` (domača stran: slika + `.hero-text`), `.features` > `.feature`, `.cta` (poziv k naročilu).
- `.gallery` > `figure.card` > `img` + `figcaption` (`<strong>` ime, `<span>` cena) + `<p>` + `<a>`.
- `.about` (slika + besedilo), `.contact-buttons`, `form.order-form` (`id="narocilo"`), `.form-row`.
- Barve so spremenljivke na `:root` (`--accent` #c2386b, `--accent-soft`, `--bg` ...). Nove dodaj tja.
- CSS je mobile-first: osnovna pravila za telefon, `@media (min-width: 560px)` in `(min-width: 860px)`.
  Polja obrazca imajo `font-size` ≥ 16px (iPhone sicer povečuje), gumbi ≥ 46px visoki.

## Obrazec

Web3Forms (`https://api.web3forms.com/submit`), ključ v `site.json` → `web3forms_key`.
Polja: ime, telefon, e-pošta, vrsta torte, datum prevzema (min. +7 dni prek JS), število oseb, opombe.
Ključ si mora uporabnik ustvariti sam na web3forms.com.

## Slike

Vzorčne slike so SVG v `static/images/` (naslovna, rojstnodnevna, cokoladna, jagodna, otroska,
porocna, cupcakes, anja). Prave fotografije: `.webp`/`.jpg`, do ~1600 px, pod 300 KB, razmerje
4:3 za torte; zamenjaj `src` v vsebini in posodobi `width`/`height`.

## Objava

Push na `main` → GitHub Actions: testi, `build.sh`, objava `docs/` na
https://milinkovicluka.github.io/Cakes_by_Anja/ . Pri lastni domeni: `static/CNAME` in basepath `/`.

## Odprte stvari

- Vsi kontaktni podatki, cene, okusi in besedilo »O meni« so vzorčni.
- `web3forms_key` je `VSTAVI-SVOJ-KLJUC` → obrazec še ne pošilja.
- Manjka slika za deljenje (`og:image`, PNG/JPG z absolutnim URL-jem).
