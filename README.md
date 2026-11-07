# Cakes by Anja

Spletna stran za domače torte **Cakes by Anja**. Zgradi jo preprost generator
statičnih strani v Pythonu (nastal v okviru tečaja
[Build a Static Site Generator](https://www.boot.dev/courses/build-static-site-generator-python)
na Boot.dev): Markdown datoteke iz `content/` pretvori v HTML strani po predlogi
`template.html` in jim doda datoteke iz `static/`.

Objavljena stran: https://milinkovicluka.github.io/Cakes_by_Anja/

## Zahteve

- Python 3.10 ali novejši (brez dodatnih knjižnic)
- Bash (na Windows: Git Bash)

## Uporaba

```bash
./test.sh    # požene teste
./main.sh    # zgradi stran v public/ in jo postreže na http://localhost:8888
./build.sh   # zgradi stran za GitHub Pages v docs/
```

Skripte delujejo na Linuxu, macOS in Windows (Git Bash).

## Zgradba projekta

| Pot | Vsebina |
| --- | --- |
| `content/` | strani v Markdownu; vsaka mapa z `index.md` postane svoja stran |
| `site.json` | ime strani, jezik in meni (`nav`) |
| `template.html` | HTML predloga (glava, meni, vsebina) |
| `static/` | `index.css` in slike (`static/images/`) |
| `src/` | generator in testi |

Strani: Domov (`content/index.md`), Torte (`content/torte/`), Kontakt (`content/kontakt/`).

## Nova stran

1. Ustvari mapo, npr. `content/galerija/`, in v njej `index.md`, ki se začne z naslovom `# Galerija`.
2. Po želji jo dodaj v meni v `site.json`: `{ "label": "Galerija", "url": "/galerija" }`.
3. Notranje povezave in slike piši z začetnim `/` (npr. `/torte`, `/images/torta.webp`),
   ker generator pred njih sam doda pravi basepath.

## Objava

Ob vsakem pushu na `main` GitHub Actions (`.github/workflows/deploy.yml`) požene
teste, zgradi stran in jo objavi na GitHub Pages. Mapi `docs/` in `public/` nista
v repozitoriju, ker se ustvarita pri gradnji.

Basepath (`/Cakes_by_Anja/`) se nastavi sam iz imena repozitorija, za
`uporabnik.github.io` je `/`. Ročni preklic: `BASEPATH="/xyz/" ./build.sh`.

## Podprt Markdown

Naslovi (`#`–`######`), odstavki, **krepko**, _ležeče_, `koda`, kodni bloki,
citati, neoštevilčeni (`- `) in oštevilčeni (`1. `) seznami, povezave in slike.
