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
| `site.json` | ime, opis, kontaktni podatki, ključ za obrazec in meni |
| `template.html` | glava z menijem in gumbom »Naroči«, noga, spodnja vrstica za telefon |
| `static/` | `index.css`, `favicon.svg` in slike v `static/images/` |
| `src/` | generator in testi |

Strani: Domov, Torte, Ponudba, O meni in Kontakt (z obrazcem za naročilo).

## Podatki strani (`site.json`)

Kontaktni podatki so zapisani samo enkrat, v `site.json`. V predlogi in v
vsebini jih uporabiš z `{{ site.kljuc }}`, npr. `{{ site.phone_display }}`.

| Ključ | Primer | Uporaba |
| --- | --- | --- |
| `phone` | `+38640123456` | povezave `tel:` (gumb Pokliči) |
| `phone_display` | `040 123 456` | prikaz številke |
| `whatsapp` | `38640123456` | WhatsApp in Viber (brez `+` in presledkov) |
| `email` | `anja@primer.si` | e-pošta |
| `instagram` | `cakesbyanja` | uporabniško ime na Instagramu |
| `location` | `Ljubljana z okolico` | kraj prevzema |
| `web3forms_key` | `xxxxxxxx-...` | ključ za obrazec (glej spodaj) |
| `description`, `tagline` | | opis za Google in slogan |

Neznan ključ (npr. tipkarska napaka) ustavi gradnjo z napako, da ne pride na stran.

## Obrazec za naročilo

Obrazec na strani Kontakt pošilja sporočila prek brezplačne storitve
[Web3Forms](https://web3forms.com): na njihovi strani vpišeš e-pošto, na katero
želiš prejemati naročila, dobiš ključ (access key) in ga vpišeš v `site.json`
pod `web3forms_key`. Dokler je tam `VSTAVI-SVOJ-KLJUC`, obrazec ne deluje.

## Slike

Zdaj so na strani vzorčne slike (`static/images/*.svg`). Ko so na voljo prave fotografije:

1. Shrani jih v `static/images/` (najbolje `.webp` ali `.jpg`, široke do ~1600 px, pod 300 KB).
2. V `content/` zamenjaj ime datoteke v `src="/images/..."`.

Velikosti slik: naslovna 1200 × 700, torte 800 × 600 (razmerje 4 : 3), Anja 600 × 700.

## Nova stran

1. Ustvari mapo, npr. `content/galerija/`, in v njej `index.md`, ki se začne z naslovom `# Galerija`.
2. Po želji jo dodaj v meni v `site.json`: `{ "label": "Galerija", "url": "/galerija" }`.
3. Notranje povezave in slike piši z začetnim `/` (npr. `/torte`, `/images/torta.webp`),
   ker generator pred njih sam doda pravi basepath.

## Podprt Markdown

Naslovi (`#`–`######`), odstavki, **krepko**, _ležeče_, `koda`, kodni bloki,
citati, neoštevilčeni (`- `) in oštevilčeni (`1. `) seznami, povezave in slike.

**HTML bloki:** blok, ki se začne z oznako (`<div`, `<form`, `<section` ...), gre
na stran nespremenjen. Tako so narejene galerija, naslovni del in obrazec.
HTML blok ne sme vsebovati prazne vrstice, ker ta konča blok.

## Telefon

Stran je narejena najprej za telefon: meni je v eni vrstici, galerija v enem
stolpcu, spodaj pa je stalna vrstica **Pokliči · WhatsApp · Naroči**. Na
računalniku (od 860 px) se spodnja vrstica skrije, gumb »Naroči torto« pa je v glavi.

## Objava

Ob vsakem pushu na `main` GitHub Actions (`.github/workflows/deploy.yml`) požene
teste, zgradi stran in jo objavi na GitHub Pages. Mapi `docs/` in `public/` nista
v repozitoriju, ker se ustvarita pri gradnji.

Basepath (`/Cakes_by_Anja/`) se nastavi sam iz imena repozitorija, za
`uporabnik.github.io` je `/`. Ročni preklic: `BASEPATH="/xyz/" ./build.sh`.
Pri lastni domeni mora biti basepath `/`.

## Še za narediti

- [ ] Pravi telefon, e-pošta, Instagram in kraj v `site.json`
- [ ] Ključ Web3Forms v `site.json`
- [ ] Prave fotografije tort, naslovne slike in Anje
- [ ] Prave cene in okusi na strani Ponudba, besedilo na strani O meni
- [ ] Slika za deljenje (Open Graph) in po želji lastna domena
