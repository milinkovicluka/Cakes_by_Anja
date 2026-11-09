# Kontakt

<!-- opis: Naročite domačo torto po telefonu, e-pošti ali prek obrazca. Bohinj, Bled, Lesce, Radovljica in Žirovnica. -->

Za naročilo torte ali vprašanja me pokličite, mi pišite ali izpolnite obrazec spodaj. Odgovorim vam čim prej.

<div class="contact-buttons">
  <a class="btn" href="tel:{{ site.phone }}">Pokliči {{ site.phone_display }}</a>
  <a class="btn btn-ghost" href="mailto:{{ site.email }}">{{ site.email }}</a>
</div>

Torte pečem za {{ site.area }}.

## Obrazec za naročilo

<form id="narocilo" class="contact-form" action="https://api.web3forms.com/submit" method="POST">
  <input type="hidden" name="access_key" value="{{ site.web3forms_key }}">
  <input type="hidden" name="subject" value="Novo povpraševanje s strani {{ site.name }}">
  <input type="checkbox" name="botcheck" class="hidden" tabindex="-1" autocomplete="off">
  <label>Ime in priimek *<input type="text" name="ime" autocomplete="name" required></label>
  <label>Telefon *<input type="tel" name="telefon" autocomplete="tel" inputmode="tel" required></label>
  <label>E-pošta<input type="email" name="email" autocomplete="email"></label>
  <div class="form-row">
    <label>Datum praznovanja *<input type="date" name="datum" id="datum" required></label>
    <label>Število kosov<input type="number" name="kosi" min="1" max="200" inputmode="numeric"></label>
  </div>
  <label>Vaše želje (okus, napis, okrasitev, alergije ...)<textarea name="opombe" rows="4"></textarea></label>
  <label class="consent"><input type="checkbox" name="soglasje" required> Strinjam se z obdelavo podatkov za odgovor na povpraševanje.</label>
  <button class="btn" type="submit">Pošlji povpraševanje</button>
  <p class="form-note">Povpraševanje ni zavezujoče. Naročilo potrdiva skupaj po telefonu ali e-pošti. Več o podatkih v <a href="/zasebnost">politiki zasebnosti</a>.</p>
</form>
<script>
  (function () {
    var d = new Date();
    d.setDate(d.getDate() + 1);
    var el = document.getElementById("datum");
    if (el) el.min = d.toISOString().slice(0, 10);
  })();
</script>
