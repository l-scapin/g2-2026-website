---
# Pagina di atterraggio del sito (raggiunta dal brand in alto a sinistra).
# Per modificare il layout: https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: "Home"
vega: true
header_type: splash #base, post, hero, image, splash — splash = pagina intera, titolo centrato
header_img: assets/images/hero_road.jpg
header_title: "Where Does the Money Go?"
subtitle: "I fondi della politica di coesione italiana: si concludono, sono a rischio, sono equi tra Nord e Sud?"

---

<div class="big-numbers big-numbers--straddle">
  <div class="stat">
    <p class="num">206.777</p>
    <p class="lbl">progetti analizzati</p>
  </div>
  <div class="stat">
    <p class="num">49%</p>
    <p class="lbl">progetti conclusi</p>
  </div>
  <div class="stat stat-sud">
    <p class="num">31%</p>
    <p class="lbl">progetti a rischio</p>
  </div>
  <div class="stat">
    <p class="num">+17&nbsp;pt</p>
    <p class="lbl">divario Nord–Sud nei conclusi</p>
  </div>
</div>

Analizziamo oltre 200.000 progetti finanziati dalla politica di coesione italiana con i
dati aperti di **OpenCoesione**, per capire dove vanno davvero i fondi pubblici e con quali esiti.
{: .lead }

# Le tre domande

<div class="qcards">
  <div class="qcard">
    <h5>Si concludono?</h5>
    <p>Quanti progetti arrivano davvero a chiusura e cosa li distingue.</p>
    <a href="{{ site.baseurl }}/eda.html">Vai all'analisi →</a>
  </div>
  <div class="qcard">
    <h5>Sono a rischio?</h5>
    <p>Quali progetti rischiano di non partire o di sforare i tempi.</p>
    <a href="{{ site.baseurl }}/xgboost.html">Vai al modello →</a>
  </div>
  <div class="qcard">
    <h5>Sono equi tra Nord e Sud?</h5>
    <p>Il divario territoriale su fondi ed esiti, il nostro messaggio centrale.</p>
    <a href="{{ site.baseurl }}/conclusions.html">Vai alle conclusioni →</a>
  </div>
</div>

<!-- Spazio per un grafico introduttivo (togli il commento e cambia il nome del file):
<div style="height: 420px">
<vegachart schema-url="{{site.baseurl}}/assets/charts/NOME_FILE.json" style="width: 100%; height: 100%"></vegachart>
</div>
-->
