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
    <p class="lbl">conclusi a oggi</p>
  </div>
  <div class="stat stat-sud">
    <p class="num">31,5%</p>
    <p class="lbl">a rischio: mai partiti o oltre scadenza</p>
  </div>
  <div class="stat">
    <p class="num">+17&nbsp;pt</p>
    <p class="lbl">divario Nord–Sud nei conclusi</p>
  </div>
</div>

Un progetto su due è arrivato a conclusione — e i cicli più recenti sono ancora in corsa. Ma
dietro la media c'è una spaccatura: al Centro-Nord si chiude quasi il **59%** dei progetti, al Sud
il **42%** — eppure è il Mezzogiorno a gestire più fondi. E non è l'incidente di un anno storto:
il divario **resiste dentro ogni ciclo** di programmazione. Da qui la nostra domanda: dove vanno
davvero i soldi pubblici, e con quali esiti?
{: .lead }

La politica di coesione è lo strumento con cui l'Unione Europea e lo Stato finanziano
interventi per ridurre i divari tra i territori: infrastrutture, ricerca, ambiente, servizi.
**OpenCoesione** è il portale che rende pubblici questi dati, progetto per progetto: noi
analizziamo i progetti da almeno 100.000 € (il PNRR resta fuori) e li leggiamo con metodi
statistici intorno a tre domande semplici ma decisive.

<!-- 🎙️ SLOT INTERVISTA — regola: MAI pubblicare virgolettati non realmente pronunciati.
     Quando l'intervista sarà fatta e autorizzata: qui UNA frase breve e d'effetto (max 2 righe);
     la citazione estesa va in conclusions.html — stessa voce che apre e chiude il racconto. -->
<div style="border-left: 4px solid #177E89; padding: 0.6rem 0 0.6rem 1.2rem; margin: 2.2rem 0;">
  <p style="font-size: 1.05rem; color: #2b2b2b; margin-bottom: 0.5rem;">
    🎙️ <strong>La voce di chi i fondi li gestisce.</strong> Stiamo intervistando un dirigente con
    esperienza diretta nella gestione di fondi pubblici: la sua lettura di questi numeri comparirà qui.
  </p>
  <p style="font-size: 0.82rem; color: #888; margin: 0;">
    Intervista in corso — 2026
  </p>
</div>

# Le tre domande

<div class="qcards">
  <div class="qcard">
    <h5>Si concludono?</h5>
    <p>Quanti arrivano davvero a chiusura — e perché i progetti grandi si fermano più spesso.</p>
    <a href="{{ site.baseurl }}/eda.html">Vai all'analisi →</a>
  </div>
  <div class="qcard">
    <h5>Sono a rischio?</h5>
    <p>Chi rischia di non partire o di sforare i tempi. Un modello impara a riconoscerli.</p>
    <!-- Quando il modello è pronto, puntare questa card a modello.html -->
    <a href="{{ site.baseurl }}/eda.html#metriche">Vai all'analisi →</a>
  </div>
  <div class="qcard qcard--sud">
    <h5>Sono equi tra Nord e Sud?</h5>
    <p>Fondi ed esiti a confronto tra Centro-Nord e Mezzogiorno: il cuore del progetto.</p>
    <a href="{{ site.baseurl }}/eda.html#divario">Vai all'analisi →</a>
  </div>
</div>

<p style="text-align: center; margin: 1.6rem 0 0.4rem;">
  <a href="{{ site.baseurl }}/conclusions.html"><strong>Di fretta? Leggi direttamente le conclusioni →</strong></a>
</p>
<p style="text-align: center; font-size: 0.85rem; color: #888;">
  In arrivo: <a href="{{ site.baseurl }}/modello.html">modello predittivo del rischio</a> ·
  <a href="{{ site.baseurl }}/clustering.html">clustering dei profili regionali</a> ·
  <a href="{{ site.baseurl }}/text-analysis.html">text analysis delle descrizioni</a>
</p>

<!-- Spazio per un grafico introduttivo (togli il commento e cambia il nome del file):
<div style="height: 420px">
<vegachart schema-url="{{site.baseurl}}/assets/charts/NOME_FILE.json" style="width: 100%; height: 100%"></vegachart>
</div>
-->

<hr>

<p style="font-size: 0.8rem; color: #888; margin-top: 1.5rem;">
  Immagine di copertina: foto di <a href="https://unsplash.com/photos/zN4mtLHkHn4" target="_blank" rel="noopener">Fahrul Azmi</a> su <a href="https://unsplash.com" target="_blank" rel="noopener">Unsplash</a>.
</p>
