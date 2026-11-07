---
name: cakes-by-anja
description: Ključni podatki za gradnjo in urejanje strani Cakes by Anja (statični generator v Pythonu, vsebina v Markdownu, objava na GitHub Pages). Uporabi pred vsakim dodajanjem ali urejanjem strani, menija, videza, slik ali generatorja v tem projektu.
---

# Cakes by Anja – kako graditi ta projekt

Spletna stran za domače torte. Jezik strani in dela z uporabnikom: **slovenščina**.

## Zgradba

- `content/**/index.md` → vsaka mapa je ena stran (`content/torte/index.md` → `/torte/`).
  Vsaka `.md` datoteka **mora** imeti naslov `# ...`, sicer gradnja pade (`no h1 header found`).
- `site.json` → `name`, `lang` (`sl`), `nav` (seznam `{ "label", "url" }`).
- `template.html` → oznake `{{ Title }}`, `{{ SiteName }}`, `{{ Lang }}`, `{{ Nav }}`, `{{ Content }}`.
- `static/` → `index.css` in `images/`; skopira se v izhodno mapo kot je.
- `src/` → generator (`main.py`, `gencontent.py`, `block_markdown.py`, `inline_markdown.py`,
  `htmlnode.py`, `textnode.py`, `copystatic.py`) in testi `test_*.py` (unittest).

## Ukazi

- `./test.sh` – testi (vedno poženi po spremembi v `src/`).
- `./main.sh` – gradnja v `public/` + strežnik na http://localhost:8888.
- `./build.sh` – produkcijska gradnja v `docs/` (basepath iz imena repozitorija → `/Cakes_by_Anja/`).
- Hitra gradnja brez strežnika: `python3 src/main.py "/" ./public`.

## Pravila za vsebino

- Notranje povezave in slike vedno z začetnim `/` (`/torte`, `/images/torta.webp`):
  `render_page` zamenja `href="/` in `src="/` z basepathom. Relativne poti se na GitHub Pages zlomijo.
- Zunanje povezave (`https://`, `mailto:`, `tel:`) delujejo normalno.
- Podprt Markdown: naslovi `#`–`######`, odstavki, `**krepko**`, `_ležeče_`, `` `koda` ``,
  kodni bloki, citati `>`, seznami `- ` in `1. `, povezave, slike `![alt](/images/x.webp)`.
- **Ni podprto:** tabele, `*ležeče*` z zvezdico, gnezdeni seznami, HTML v Markdownu.
- Neparni `**` ali `` ` `` sprožijo napako `invalid markdown: unmatched ...`.
- Bloke ločuje prazna vrstica; seznam mora imeti vse vrstice z istim začetkom.
- Slog besedila: vikanje (»vi«, »naročite«), topel in preprost ton.
- Slike: format `.webp`, shranjene v `static/images/`.

## Videz

`static/index.css` uporablja spremenljivke na `:root`: `--bg` (#fff8f0), `--text` (#4a3b3b),
`--accent` (#c2386b), `--accent-soft` (#f9dde6). Pisava Georgia, širina 760px.
Nove barve dodaj kot spremenljivke, ne neposredno.

## Objava

Push na `main` → `.github/workflows/deploy.yml` požene teste, `build.sh` in objavi `docs/`
na GitHub Pages: https://milinkovicluka.github.io/Cakes_by_Anja/
`docs/` in `public/` sta v `.gitignore`.

## Odprte stvari

- Kontakt (`content/kontakt/index.md`) ima še nadomestne podatke `anja@example.com` in `000 000 000`.
- Torte so zaenkrat primeri brez slik; `static/images/` je prazna.
