---
layout: default
title: "Conclusioni"
vega: true
show_sidetoc: true
header_type: hero #base, post, hero, image, splash
header_img: assets/images/hero_conclusions.jpg
header_img_position: "center 34%" # centra la spirale (il fulcro dell'immagine è in alto-centro)
header_title: "Conclusioni"
subtitle: "Sintesi dei risultati e prossimi passi"
---

<div class="full-width-wrapper">
    <img src="{{ site.baseurl }}/assets/images/header.svg" alt="sbd-pattern" class="full-width-image">
</div>

Abbiamo letto oltre 200.000 progetti della politica di coesione con tre domande in testa: si
concludono, sono a rischio, sono equi tra Nord e Sud? Ecco cosa dicono i dati — e, altrettanto
importante, cosa ancora **non** possono dire.
{: .lead }

# I progetti si concludono?

Circa **metà** dei progetti arriva a chiusura, ma la media nasconde due dipendenze forti. La prima
è l'**età del ciclo**: i cicli ormai chiusi (2000-06 e 2007-13) sono conclusi al 76% e 66%, mentre
il 2021-2027 è appena partito (5%). La seconda è la **dimensione**: si passa dal 53,6% di conclusione
dei progetti piccoli al 13,8% di quelli oltre i 50 milioni, che assorbono anche molto meno. La lettura
onesta è che i risultati vanno pesati per importo, non contati per numero. Il dettaglio è nella
[pagina EDA]({{ site.baseurl }}/eda.html).

# Sono a rischio?

Quasi un terzo dei progetti (**31,5%**) è a rischio — mai partito, oppure in corso con la scadenza già superata —
e il rischio si concentra sui progetti medio-grandi e sui cicli recenti. Ma la domanda vera è: il
territorio conta *di per sé*, o è solo un effetto di dimensione, ciclo e tema?

<!-- ⚠️ SLOT MODELLO — da completare con i risultati reali del Notebook 02.
     Scritto per reggere QUALSIASI esito: scegliere l'esito vero, non piegare i dati alla frase.
     NOTA METODO: la Random Forest dà l'importanza delle variabili (feature importance/SHAP),
     NON stime "a parità di condizioni" (+X punti, odds ratio). Se volete anche quella frase,
     affiancate una regressione logistica semplice: è lei a dare quel numero. -->
> **[DA COMPLETARE — risultato del modello]** Il **modello multivariato**
> (pagina [modello]({{ site.baseurl }}/modello.html)) mette territorio, dimensione, ciclo e tema
> sullo stesso piano e misura quanto ciascuno pesa nel predire il rischio. **[Esito A: il
> territorio resta tra i fattori più rilevanti → il divario non si spiega con la composizione dei
> portafogli. / Esito B: pesano soprattutto dimensione e ciclo → più che un "problema Sud", un
> problema di come sono fatti i progetti.]** In entrambi i casi è una notizia. Nello stesso modello
> verifichiamo il ruolo del numero di enti coinvolti, la cui correlazione grezza con i ritardi era
> praticamente nulla nell'EDA (≈ −0,04): **[risultato]**.

# Fondi ed esiti sono equi (Nord / Sud)?

È il cuore del progetto, ed è la risposta più netta. Il Centro-Nord conclude il **58,8%** dei progetti
contro il **41,6%** del Sud, ed è a rischio molto meno (**20,1% vs 40,3%**); sull'assorbimento la
distanza è più contenuta (**0,75 vs 0,69**). Non è una questione di soldi in meno: il Mezzogiorno
gestisce anzi **più fondi** (215 vs 79 miliardi €), coerentemente con la missione redistributiva della
coesione. E non dipende dal calendario: verificando il divario *dentro ogni ciclo* di programmazione,
in tutti i cicli il Centro-Nord conclude di più. Il gap è **persistente** — quanto sia *strutturale*,
cioè non riducibile alla composizione per dimensione e tema dei portafogli, lo dirà il modello.
A livello regionale il gradiente è quasi senza eccezioni: in coda la Sicilia (31% concluso, 50% a
rischio), in testa la Liguria (76%).

<!-- TODO (fattibile subito, è ancora EDA): incrocio macroarea × classe di importo.
     Se il divario regge dentro ogni classe di importo, rafforzare qui la frase.
     Usare la parola "strutturale" solo dopo quel controllo + il modello. -->

<!-- 🎙️ SLOT INTERVISTA — regola: MAI pubblicare virgolettati non realmente pronunciati.
     Qui andrà la CITAZIONE ESTESA autorizzata; in home la stessa voce apre con una frase breve.
     In attesa (o in alternativa): una citazione REALE da fonti pubblicate, con riferimento —
     es. relazioni della Corte dei Conti sui fondi SIE, rapporti Banca d'Italia o SVIMEZ
     sulla capacità amministrativa. -->
<div style="border-left: 4px solid #D1573B; padding: 0.6rem 0 0.6rem 1.2rem; margin: 2rem 0;">
  <p style="font-size: 1.05rem; color: #2b2b2b; margin-bottom: 0.5rem;">
    🎙️ <strong>La voce di chi i fondi li gestisce.</strong> Qui entrerà l'intervista a un dirigente
    con esperienza diretta nella gestione di fondi pubblici: che cosa vede, dal campo, dietro questi numeri?
  </p>
  <p style="font-size: 0.82rem; color: #888; margin: 0;">
    Intervista in corso — 2026
  </p>
</div>

# Limiti dell'analisi

Tre avvertenze prima di leggere tutto questo come una verità causale. Primo: le differenze descrittive
non bastano da sole, ed è per questo che il passo decisivo è il modello. Secondo: il **ritardo** è
misurato quasi solo sui progetti con una fine effettiva, quindi le analisi sui tempi vanno prese con
prudenza. Terzo: qui guardiamo la sola politica di **coesione** — il **PNRR resta fuori**, e confrontare
i due canali richiede cautela metodologica (regole, tempistiche e sistemi di monitoraggio diversi).

# Cosa ci portiamo a casa

Tre messaggi restano in piedi qualunque cosa dica il modello. Primo: **contare i progetti inganna**
— vanno pesati per importo, e i progetti grandi sono l'anello debole del sistema (sopra i 50 milioni
si conclude il 13,8%). Secondo: c'è un **falso colpevole** — la complessità di governance, misurata
dal numero di enti coinvolti, non correla con i ritardi. Terzo: il **divario Nord-Sud non è un
incidente di percorso** — persiste in ogni ciclo, nonostante al Sud arrivino più fondi. La leva più
concreta che emerge dai dati descrittivi non è *quanti* soldi arrivano, ma *come sono disegnati* i
progetti che li spendono.

<!-- ⚠️ FRASE FINALE — da chiudere col verdetto del modello: territorio o dimensione? -->
**[DA COMPLETARE — la chiusura del racconto: quale dei due indiziati pesa di più?]**

# Prossimi passi

Il **modello multivariato** pesa territorio e dimensione sullo stesso piano ed è il naturale
completamento di questa sintesi. Accanto, la **text analysis** verifica se dalle descrizioni dei
progetti emergano parole associate all'esito, e il **clustering** raggruppa i profili regionali. Il
confronto con il **PNRR**, se i dati risulteranno comparabili, è l'estensione più ambiziosa.

<hr>

<p style="font-size: 0.8rem; color: #888; margin-top: 1.5rem;">
  Immagine di copertina: foto di <a href="https://unsplash.com/photos/zBrnXi2IgpY" target="_blank" rel="noopener">Rodrigo Kugnharski</a> — Parco del Portello, Milano, su <a href="https://unsplash.com" target="_blank" rel="noopener">Unsplash</a>.
</p>
