---
layout: default
title: "EDA"
vega: true
plotly: true
show_sidetoc: true
header_type: hero #base, post, hero, image, splash
header_img: assets/images/hero_eda.jpg
header_img_position: center
header_title: "Analisi Esplorativa dei Dati"
subtitle: "Qualità dei dati, la metrica del rischio e i primi pattern"
---

<div class="full-width-wrapper">
    <img src="{{ site.baseurl }}/assets/images/header.svg" alt="sbd-pattern" class="full-width-image">
</div>

La fonte del nostro dataset è **OpenCoesione**, un progetto di open government che raccoglie i dati relativi ai progetti finanziati con le politiche di coesione. Abbiamo scelto di concentrare la nostra analisi solo su progetti con un valore finanziato **maggiore o uguale a 100.000 €**. 
In totale, il nostro dataset è composto da **206.777 progetti**. Nella nostra esplorazione preliminare, abbiamo cercato di definire quali fossero **a rischio** e di isolarne le **caratteristiche principali**.  
{: .lead }

# Qualità e preparazione dei dati

Il dataset non ha righe duplicate: ogni progetto è identificato in modo **univoco** dalla coppia CUP + codice locale. 

I **valori mancanti** nel dataset dipendono dalla sua struttura e non vanno considerati come errori. Per esempio, il _ritardo_ e la _data di fine effettiva_ sono valori assenti sui progetti non ancora conclusi. Oppure, progetti interamente finanziati con fondi nazionali (FSC, PAC) non hanno valori relativi alle _descrizioni tematiche_ e _fondo europeo_.



# La metrica: quando un progetto è a rischio {#metriche}

Nei dati ufficiali non esiste un'etichetta di **"fallimento"**: un progetto resta aperto finché non viene formalmente chiuso o definanziato. Abbiamo quindi optato per una **classificazione binaria operativa** che fotografa la presenza di un'anomalia procedurale alla data di riferimento del **31 dicembre 2025**.

<div class="def-box">
  <p class="def-box__label">La nostra variabile target</p>
  <h4>Come definiamo un progetto «a rischio»?</h4>

  <p>Un progetto è etichettato come <strong>«a rischio»</strong> se:</p>
  <p>
    <strong>1 · Non è mai partito:</strong> risulta ancora «non avviato» (16.261 progetti, 7,9%), <em>oppure</em><br>
    <strong>2 · È oltre la scadenza:</strong> risulta «in corso» ma ha già superato la data di fine prevista (51.237 progetti, 24,8%).
  </p>

  <p>In totale parliamo di <strong>67.498 progetti (32,6%)</strong>. Raggruppare sotto la stessa variabile sia i ritardi recenti sia i blocchi pluriennali è una <strong>scelta metodologica precisa</strong>: anziché introdurre una soglia arbitraria oltre la quale considerare un progetto "definitivamente morto" (soglia smentita nei fatti da opere che si sbloccano anche dopo anni), cataloghiamo come <em>a rischio</em> qualsiasi iter che ha deviato rispetto al cronoprogramma originario.</p>

</div>


## Dove passano i fondi

Prima di osservare i progetti attraverso la lente della nostra variabile target, vediamo la **distribuzione dei fondi** attraverso un **diagramma di Sankey**. 

Nel grafico, ogni flusso ha uno **spessore proporzionale** ai fondi pubblici netti (in miliardi di €), partendo da ciascuna possibile **fonte di finanziamento** (FESR, FSE, FSC, Fondo di rotazione, PAC, Regione), passando per il **territorio** (Mezzogiorno, Centro-Nord) e finendo su ciascun **tema** del progetto. 
Da questa visualizzazione possiamo vedere come al Mezzogiorno la coesione è più **nazionale** (FSC) che europea (FESR), e i **trasporti** sono il tema che assorbe la fetta maggiore del finanziamento.
Inoltre, in maniera coerente con la missione redistributiva delle politiche di coesione, al Mezzogiorno vengono allocati **molti più fondi** (215 contro 79 mld €). 

<figure class="fig-home">
  <iframe src="{{ site.baseurl }}/assets/charts/plotly/sankey_fondi.html"
          title="Diagramma di Sankey: il percorso dei fondi dalla fonte al territorio al tema"
          style="width: 100%; height: 750px; border: none;"
          loading="lazy"
          scrolling="no"></iframe>
</figure>


È importante notare che nonostante questo sbilanciamento nella attribuzione dei fondi, il numero di progetti risulta comunque **bilanciato** per ciascuna macro-area.

Infatti, sul totale dei progetti analizzati, il **56%** è al Mezzogiorno, mentre il **44%** al Centro-Nord.

![Quota di progetti nel Centro-Nord e nel Mezzogiorno]({{ site.baseurl }}/assets/images/eda/04b_bilanciamento.png){: .img-fluid }


# Dimensione e tema 

Per esplorare la dimensione del rischio, abbiamo deciso di osservare due features specifiche: la **dimensione**, ovvero la quantità di fondi destinati ai progetti, e il **tema**.

**Dimensione.** Abbiamo diviso la dimensione per classi di importo. Questo ci consente di osservare che il rischio non cresce necessariamente con la taglia del progetto. La distribuzione del rischio, infatti, disegna una campana. Sale dal 29,4% dei progetti più piccoli fino al 43,9% della fascia 5-10 milioni, per poi scendere nuovamente (42,9% fra 10 e 50 milioni, 38,5% sopra i 50). 

Il punto più critico sono i **progetti medio-grandi**, quelli che potrebbero essere abbastanza complessi da accumulare ritardo, ma non abbastanza grandi da ricevere un’attenzione particolare.

![Percentuale di progetti a rischio per classe di importo]({{ site.baseurl }}/assets/images/eda/05_dimensione_rischio.png){: .img-fluid }

Resta un dato di peso da tenere presente: i progetti piccoli (100-500k) sono il 70% del totale ma circa 31 dei 315 miliardi, mentre i 623 progetti sopra i 50 milioni ne valgono da soli 120. 

**Tema.** Il tema maggiormente associato ai progetti a rischio è la **competitività delle imprese** (39,6% a rischio), seguito da **trasporti e mobilità** (37,4%) e **ambiente** (35,2%). 

Quelli meno a rischio sono: **reti e servizi digitali** (21,8%), **energia** (24,2%) e **capacità amministrativa** (26,2%). I **trasporti** meritano attenzione perché muovono i fondi maggiori, quasi 100 miliardi su 315, praticamente un terzo di tutto il denaro.


![Rischio per tema]({{ site.baseurl }}/assets/images/eda/09_tema.png){: .img-fluid }


# Divario territoriale: Centro-Nord/Mezzogiorno {#divario}

Continuando la nostra analisi sul rischio e concentrandoci sulla localizzazione dei progetti, vediamo che il 42% dei progetti del Mezzogiorno è **«a rischio»**, mentre nel Centro-Nord solo il 20,5%.

Sui progetti mai avviati le due aree sono quasi pari, 7,2% al Mezzogiorno, 8,8% al Centro-Nord. Il **divario principale**, dunque, si trova nei progetti **in ritardo**: al Mezzogiorno, sono il 34,8%, al Centro-Nord l’11,7%. Si tratta di una differenza di circa un triplo.


![Esiti per macroarea territoriale]({{ site.baseurl }}/assets/images/eda/04_territorio.png){: .img-fluid }

Il divario è osservabile anche dentro ogni **ciclo di programmazione**: in _tutti_ i cicli il Mezzogiorno è più a rischio, con uno scarto di **30 punti percentuali** nel ciclo 2014-2020. 
Per un’analisi più approfondita del ruolo del territorio nella definizione di questo scarto, a parità di dimensione, tema e tipo di intervento, rimandiamo alla  [**regressione multivariata**]({{ site.baseurl }}/regressione.html).

![Divario di rischio Nord-Sud, per ciclo]({{ site.baseurl }}/assets/images/eda/07_divario_per_ciclo.png){: .img-fluid }

## La mappa regionale 

Per non fermarci alla semplice distinzione tra macro-aree, abbiamo analizzato il rischio anche a **livello regionale**: il gradiente da Nord a Sud si conferma, ma con eccezioni in entrambe le direzioni.

In coda c’è la Sicilia con il 53,8%, staccata di tredici punti dalla seconda, la Campania (40,5%): più di un progetto su due. A queste due seguono Calabria (39,8%) e Puglia (38,5%). In testa la Liguria con il 9,2%, poi Valle d’Aosta (15,5%), Molise (16,5%) e Veneto (16,6%).

**Le eccezioni.** Nel Centro-Nord, Marche (31,4%) e Lazio (27,6%) hanno progetti con un tasso di rischio peggiore di quattro regioni del Mezzogiorno: nel caso delle Marche il motivo si legge nella scomposizione, perché il 16,2% dei loro progetti non è mai partito, il valore più alto d’Italia, mentre il 15,2% fuori tempo è nella norma del Centro-Nord. Dall’altro lato il Molise è davanti a Lombardia, Piemonte e Veneto. Il territorio, dunque, pur dando una chiave di lettura importante, non spiega in maniera completa le ragioni del rischio. 

<div style="width: 100vw; margin-left: calc(50% - 50vw); display: flex; justify-content: center; margin-top: 2.5rem; margin-bottom: 1.5rem;">
  <figure class="fig-home" style="margin: 0; width: min(960px, 96vw); display: flex; flex-direction: column;">
    <iframe src="{{ site.baseurl }}/assets/charts/interactive/dashboard_regioni.html"
            title="Dashboard interattiva delle regioni"
            style="width: 100%; height: 670px; border: none; transform: translateX(30px);"
            loading="lazy"></iframe>
    <figcaption style="transform: translateX(30px);">
      La dashboard è interattiva. Dal menu a tendina si può scegliere quale vista del rischio mostrare: il totale, la sola quota di progetti mai avviati o la sola quota fuori tempo massimo. La mappa si ricolora e la classifica regionale si aggiorna; passando il mouse su una regione la si evidenzia in entrambe le viste. Cambiando voce si vede che le regioni non si dispongono nello stesso ordine: due regioni con lo stesso rischio complessivo possono avere problemi opposti.
    </figcaption>
  </figure>
</div>



# Numero di enti coinvolti e ritardi

Abbiamo anche considerato l’**ipotesi** che **più enti coinvolti** in un progetto possano contribuire al ritardo, considerando eventuali **difficoltà di coordinamento** fra soggetti. 

Dall’analisi emerge che la **correlazione** fra il numero di enti e il ritardo è **praticamente nulla (coefficiente di correlazione di Pearson ≈ −0,04)**. 

Ovviamente, in questo caso il ritardo è misurato quasi solo sui progetti conclusi: per un’analisi più approfondita di questo aspetto rimandiamo alla regressione multivariata, dove il numero di enti entra tra i predittori sul **rischio** (che include anche i progetti mai partiti).


![Numero di enti e ritardo medio]({{ site.baseurl }}/assets/images/eda/12_governance.png){: .img-fluid }

# Correlazioni 

In maniera preliminare alla **costruzione di un modello**, abbiamo cercato di identificare le variabili che portano **informazione diversa** e più significativa. 

La prima matrice mette a confronto tutte le variabili numeriche continue e fa emergere tre gruppi ridondanti: le **grandezze finanziarie assolute** (finanziamento, pagamenti, costo realizzato, con correlazioni fino a 0,90), i due **contatori di governance** (numero di attuatori e numero di enti, di fatto la stessa variabile: 0,98) e le **quote UE** e **Stato**, quasi complementari per costruzione (−0,72). Per la costruzione del modello, prenderemo da ciascun gruppo una sola variabile. 

![Matrice di correlazione di tutte le variabili continue]({{ site.baseurl }}/assets/images/eda/10_correlazione.png){: .img-fluid }

Tenendo in considerazione solo 4 di queste variabili, possiamo calcolare la seguente matrice. 

![Matrice di correlazione delle sole variabili note alla partenza]({{ site.baseurl }}/assets/images/eda/10c_correlazione_ripulita.png){: .img-fluid }

La correlazione più alta è **0,20**. Le quattro variabili raccontano cose diverse, e i coefficienti del modello si potranno leggere uno per uno senza il sospetto che si stiano rubando informazione a vicenda.

Da qui partono le analisi successive, che lavorano tutte sullo stesso insieme con qualche adattamento: il [clustering]({{ site.baseurl }}/clustering.html)
prende come variabili il logaritmo in base 10 del finanziamento totale e della quota privata,mentre la [regressione]({{ site.baseurl }}/regressione.html) e il Random Forest usano
l'importo suddiviso in fasce.

# In sintesi 

Un progetto su tre (32,6%) è a rischio, e in aggregato il problema è l’esecuzione più che l’avvio: il 24,8% è partito e ha già sforato la scadenza, il 7,9% non è mai partito. Il rischio si concentra sui progetti medio-grandi (picco del 43,9% fra 5 e 10 milioni), e riguarda alcuni temi specifici. 

Il divario territoriale è netto (42,0% contro 20,5%) ed è osservabile in ciascun ciclo di finanziamenti. La complessità di governance, invece, non spiega i ritardi.

Restano due avvertenze prima di trarre conclusioni causali: le differenze descrittive non bastano. Il passo successivo è la  [**regressione multivariata**]({{ site.baseurl }}/regressione.html), che stima il peso del territorio a parità di dimensione, tema, tipo di intervento e fonte di finanziamento.

