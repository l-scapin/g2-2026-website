---
# Landing = ARTICOLO (una sola pagina lunga, scrollytelling con ancore, deciso il 14/07/2026).
# La navbar punta alle ancore: #il-problema · #perche-succede · #cosa-fare
# Per modificare il layout: https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: "Home"
vega: true
header_type: splash #base, post, hero, image, splash. Splash = pagina intera, titolo centrato
header_img: assets/images/hero_road.jpg
header_title: "Where Does the Money Go?"
subtitle: "315 miliardi per riequilibrare l'Italia. Ma i progetti si fermano proprio dove servono di più: al Sud il rischio è doppio che al Nord."

---

<!-- ═══════════════════════════════════════════════════════════════════
     Articolo in 3 atti. RISCRITTO il 24/07/2026 sulla revisione del gruppo
     (Data Journalism e struttura/Articolo_corretto.md). Rispetto alla bozza precedente:
     · Atto I: tolto il paragrafo narrativo "protagonista/oggetto del desiderio".
     · Atto II: identikit ristrutturato in Dimensione/Ciclo/Tema; antagonista attribuito
       all'intervistato (Giuseppe Magnifico, CNR) per nome; tolto il box "network".
     · Atto III: bicchiere alleggerito (via i tassi di conclusione); TOLTE la sezione
       "Cosa ci portiamo a casa", la frase-verdetto, la sezione "Limiti" e il box "effetto domino".
     · Intervista: ridotta a TRE citazioni (capacità in Atto II, bicchiere e Bologna in Atto III).
     🎙️ INTERVISTA = citazioni VERBATIM, MAI virgolettati inventati. ⚠️ Il gruppo ha scelto di
        NOMINARE l'intervistato: DA AUTORIZZARE prima della consegna, e da verificare che il nome
        sia corretto (nella trascrizione "Giuseppe Magnifico" compare anche come nome di esempio).
        Caveat PNRR/fondi nazionali ora solo implicito ("meccanismi del finanziamento pubblico").
     ⚠️ La fascia big-numbers e i grafici 07_divario_per_ciclo / 08_regioni usano ancora la metrica
        "conclusi": vanno adeguati quando si completa il passaggio a "rischio" (task in sospeso).
     Numeri con data di riferimento 31/12/2025 (snapshot del dataset). Non arrotondare 32,6 → 32.
     ═══════════════════════════════════════════════════════════════════ -->

<div class="big-numbers big-numbers--straddle big-numbers--bleed">
  <div class="stat stat-money">
    <p class="num">315&nbsp;mld&nbsp;€</p>
    <p class="lbl">di soldi pubblici in gioco</p>
  </div>
  <div class="stat">
    <p class="num">206.777</p>
    <p class="lbl">progetti analizzati</p>
  </div>
  <div class="stat">
    <p class="num">49%</p>
    <p class="lbl">conclusi a oggi</p>
  </div>
  <div class="stat stat-sud">
    <p class="num">32,6%</p>
    <p class="lbl">a rischio: mai partiti o oltre scadenza</p>
  </div>
  <div class="stat">
    <p class="num">+17&nbsp;pt</p>
    <p class="lbl">divario Nord–Sud nei conclusi</p>
  </div>
</div>

Un progetto su due finanziato con i fondi delle politiche di coesione è arrivato a conclusione, e
quelli più recenti sono ancora in corsa. Ma dietro la media c'è una spaccatura: al Centro-Nord si
chiude quasi il **59%** dei progetti, al Sud il **42%**, eppure è il Mezzogiorno a gestire più
fondi. E non è l'incidente di un anno storto: il divario **resiste dentro ogni ciclo** di
programmazione.
{: .lead }

# Le politiche di coesione {#coesione}

Sono lo strumento con cui l'Unione Europea e lo Stato italiano finanziano interventi per ridurre i divari tra territori: infrastrutture, ricerca, ambiente, scuole, servizi. 

L'origine di questi finanziamenti risiede nei fondi europei, affiancati da un consistente cofinanziamento nazionale (il solo Fondo Sviluppo e Coesione vale circa 99 miliardi di euro). In entrambi i casi la fonte ultima è la stessa: le **tasse di tutti**. Nei progetti monitorati da **OpenCoesione** (il portale pubblico che ne raccoglie i dati) si raggiungono oltre **315 miliardi di euro** di finanziamento pubblico (fotografati al **31 dicembre 2025**).

Questi progetti si distribuiscono in tutta Italia e si articolano su cicli di programmazione di sette anni (dal 2000-2006 al 2021-2027), destinando una quota maggiore di risorse al Mezzogiorno in coerenza con la propria missione redistributiva. L'obiettivo dichiarato è l'**equità territoriale**: far sì che la qualità dei servizi a disposizione di un cittadino non dipenda dalla provincia in cui risiede. 

Il nostro lavoro nasce per rispondere a tre quesiti fondamentali: capire quali progetti **non vanno a buon fine**, individuare i **fattori** che ne condizionano l'esito e verificare se sia possibile **prevedere** le opere potenzialmente più a rischio fin dal primo giorno di cantiere. 

Per farlo, abbiamo ristretto il campo ai progetti con un importo pari ad almeno 100.000 euro: una scelta che ci permette di analizzare ben 249 miliardi di euro, pari al **93% delle risorse totali**.

Il grafico Sankey ricostruisce il percorso di questi 249 miliardi: dalla fonte (europea o nazionale), attraverso il territorio di destinazione, fino al tema dell'intervento. Emerge subito un primo marcato squilibrio finanziario, coerente con lo scopo delle politiche di coesione: il **73% delle risorse** è destinato al Mezzogiorno, mentre solo il **27%** va al Centro-Nord.

<figure class="fig-home">
  <iframe src="{{ site.baseurl }}/assets/charts/plotly/sankey_fondi.html"
          title="Diagramma di Sankey: il percorso dei fondi dalla fonte al territorio al tema"
          style="width: 100%; height: 520px; border: none;"
          loading="lazy"></iframe>
  <figcaption>
    Il percorso dei fondi: da ogni <strong>fonte</strong>, europea o nazionale (FSC, PAC,
    rotazione), al <strong>territorio</strong>, fino al <strong>tema</strong>. Lo spessore dei flussi
    è proporzionale ai fondi pubblici. Passa il mouse sui flussi per i valori;
    la legenda completa delle fonti è <a href="{{ site.baseurl }}/eda.html#dove-passano-i-fondi">nell'EDA</a>.
  </figcaption>
</figure>

A fronte di un volume di risorse nettamente sbilanciato verso il Sud, il **numero di progetti** risulta invece distribuito in modo quasi paritario tra le due macro-aree (56,0% al Mezzogiorno contro 44,0% al Centro-Nord). Questa sostanziale equivalenza di numerosità campionaria è un elemento metodologico cruciale, poiché garantisce l'assenza di bias nei confronti statistici successivi.

<figure class="fig-home">
  <img src="{{ site.baseurl }}/assets/images/eda/04b_bilanciamento.png"
       alt="Barra divisa in due: il 44,0% dei progetti sta nel Centro-Nord e il 56,0% nel Mezzogiorno, quindi vicino alla metà esatta">
  <figcaption>
    La distribuzione dei progetti: dei <strong>oltre 200.000</strong> interventi localizzati, il <strong>44,0%</strong> si trova nel Centro-Nord (89.831) e il <strong>56,0%</strong> nel Mezzogiorno (114.229). I <strong>fondi</strong>, al contrario, sono fortemente concentrati a Sud (<strong>73% contro 27%</strong>), come evidenziato nel diagramma precedente.
  </figcaption>
</figure>

Per esplorare ed elaborare questa massa di dati abbiamo applicato una serie di metodologie statistiche e di Machine Learning, i cui dettagli ed esiti tecnici sono approfonditi nelle sezioni dedicate del menu «Le analisi»:
[esplorazione dei dati]({{ site.baseurl }}/eda.html), [clustering]({{ site.baseurl }}/clustering.html),
[regressione]({{ site.baseurl }}/regressione.html) e [Random Forest]({{ site.baseurl }}/random-forest.html).



# Il problema: i progetti si fermano dove servono di più {#il-problema}

Cosa succede ai progetti analizzati? Per cercare di capirlo abbiamo definito una variabile che ci aiutasse a identificare quelli potenzialmente più problematici. 

<div class="def-box">
  <p class="def-box__label">La nostra variabile target</p>
  <h4>Come definiamo un progetto «a rischio»?</h4>

  <p>Nei dati ufficiali non esiste un'etichetta di "fallimento": un progetto resta aperto finché non viene formalmente chiuso o definanziato. Abbiamo quindi optato per una <strong>classificazione binaria operativa</strong> che fotografa la presenza di un'<strong>anomalia procedurale</strong> alla data di riferimento del <strong>31 dicembre 2025</strong>.</p>

  <p>Un progetto è quindi etichettato come <strong>«a rischio»</strong> se:</p>
  <p>
    <strong>1 · Non è mai partito:</strong> risulta ancora «non avviato» (16.261 progetti, 7,9%), <em>oppure</em><br>
    <strong>2 · È oltre la scadenza:</strong> risulta «in corso» ma ha già superato la data di fine prevista (51.237 progetti, 24,8%).
  </p>

  <p>In totale parliamo di <strong>67.498 progetti (32,6%)</strong>. Raggruppare sotto la stessa variabile sia i ritardi recenti sia i blocchi pluriennali è una <strong>scelta metodologica precisa</strong>: anziché introdurre una soglia arbitraria oltre la quale considerare un progetto "definitivamente morto" (soglia smentita nei fatti da opere che si sbloccano anche dopo anni), cataloghiamo come <em>a rischio</em> qualsiasi iter che ha deviato rispetto al cronoprogramma originario.</p>

  <p class="def-box__note">
    <strong>In sintesi:</strong> «A rischio» identifica un'anomalia di percorso ancora aperta, non un verdetto di fallimento. Non riguarda chi ha chiuso in ritardo, ma chi oggi non sta rispettando i tempi previsti.
  </p>
</div>

Le cifre con cui abbiamo a che fare sono enormi: nei progetti a rischio sono impegnati
**122,5 miliardi di euro** di finanziamento pubblico (più di un terzo dell'intero portafoglio),
di cui risultano pagati finora solo 45,5. Ci sono **26,3 miliardi** fermi in 16.261 progetti
**mai avviati**, con zero pagamenti. E la geografia del denaro fermo ricalca quella del bisogno:
**99,4 miliardi a rischio nel Mezzogiorno**, 18,5 nel Centro-Nord.

Si tratta della conseguenza di un numero maggiore di fondi stanziati per il Sud? Solo parzialmente. In realtà, anche in termini **relativi** (percentuale di progetti "a rischio" rispetto al numero totale di progetti della regione regione), **il divario rimane significativo**: si passa dal **9,2%** della Liguria al **53,8%** della Sicilia. 

<div style="width: 100vw; margin-left: calc(50% - 50vw); display: flex; justify-content: center; margin-top: 2.5rem; margin-bottom: 1.5rem;">
  <iframe src="{{ site.baseurl }}/assets/charts/interactive/dashboard_regioni.html"
          title="Dashboard interattiva delle regioni"
          style="width: min(960px, 96vw); height: 720px; border: none; transform: translateX(30px);"
          loading="lazy"></iframe>
</div>

Inoltre, questo divario persiste in ognuno dei cicli di programmazione analizzati. 

<!-- ✅ Migrato al rischio il 25/07 (figura rigenerata dal nb 01 §3.1: prima era sui conclusi). -->
<figure class="fig-home">
  <img src="{{ site.baseurl }}/assets/images/eda/07_divario_per_ciclo.png"
       alt="Barre appaiate Centro-Nord e Mezzogiorno: in ogni ciclo di programmazione il Mezzogiorno ha una quota maggiore di progetti a rischio">
</figure>

Un paese **disunito** è un paese **fragile** e **meno competitivo**, più esposto alle dinamiche di potere sovranazionali. In gioco ci sono due cose molto importanti: **i nostri soldi**, e come li stiamo impiegando, e un godimento dei **diritti** che sia equo e giusto per tutti sull'intero territorio nazionale. 


# Le cause {#perche-succede}

## L'identikit del rischio
Cosa caratterizza un progetto a rischio, al di là della regione in cui si trova? 
Proviamo quindi a costruire un identikit dei progetti a rischio concentrandoci su 2 caratteristiche: dimensione e tema. 


**Dimensione.** Il rischio cresce con la quantità di fondi stanziati per ciascun progetto, fino a raggiungere un picco nei progetti **medio-grandi**, quelli fra 5 e 10 milioni, a rischio nel **43,9%** dei
casi. I progetti ancora più grandi, mostrano un'inversine del trend, risultando a rischio nel 38,5% dei casi. Possiamo ipotizzare che alle opere più grandi venga riservata un'attenzione particolare. 

<!-- GRAFICI · dimensione (campana) e persistenza del divario per dimensione. -->

<figure class="fig-home">
  <img src="{{ site.baseurl }}/assets/images/eda/05_dimensione_rischio.png"
       alt="Grafico a barre: la percentuale di progetti a rischio sale fino al 43,9% nella fascia 5-10 milioni e poi ridiscende">
  <figcaption>
    Il rischio non cresce all'infinito con la taglia: disegna una campana. Dal 29,4% dei progetti
    piccoli (100–500k €) sale al <strong>43,9% della fascia 5-10 milioni</strong>, poi ridiscende
    al 38,5% sopra i 50 milioni. Il punto più debole sono i progetti medio-grandi.
  </figcaption>
</figure>


**Tema.** Alcuni temi risultano più a rischio di altri: la **competitività delle imprese** (39,6%),
i **trasporti** (37,2%) e l'**ambiente** (34,9%). 

![Rischio per tema]({{ site.baseurl }}/assets/images/eda/09_tema.png){: .img-fluid }

Verrebbe da pensare che i progetti con più soggetti coinvolti
(più enti, più tavoli, più firme) siano i più fragili. I dati dicono di no: la correlazione
tra numero di enti e rischio è praticamente nulla, e i progetti con più di 5 enti sono anzi i
*meno* a rischio.



## La regressione logistica

Per approfondire il ruolo specifico delle diverse variabili in questa dinamica, ci vengono incontro i risultati del
**modello multivariato** (pagina [regressione]({{ site.baseurl }}/regressione.html)), che confronta i progetti a parità di **tipo di intervento** (lavori pubblici, incentivi a imprese, contributi ad altri soggetti, acquisto di beni...), **tema**,
**dimensione** e **fonte di finanziamento**, rispetto alla variabile target "a rischio" che abbiamo definito prima. 

Stando al modello per un progetto
del Mezzogiorno il rapporto tra la probabilità di incepparsi e quella di non incepparsi è **quasi il
triplo** che al Centro-Nord. 

Per quanto riguarda il **tipo** di intervento, il fattore di rischio aumenta in progetti che prevedono l'erogazione di contributi ad altri soggetti o la realizzazione di lavori pubblici, rispetto a progetti finalizzati all'acquisto di beni. 

Inoltre i progetti finanziati con **fondi europei**, a prescindere dalla quantità del finanziamento, sono meno a rischio, a parità di tutto il resto. Questo potrebbe essere dovuto al fatto che arrivano con scadenze vincolanti e regole di rendicontazione più restrittive. 


<!-- GRAFICO · forest plot divulgativo (make_mod_landing_or.py). -->

<figure class="fig-home">
  <img src="{{ site.baseurl }}/assets/images/modello/mod_landing_or.png"
       alt="Grafico a pallini con intervalli di confidenza: il Mezzogiorno è il fattore più forte a 2,80, seguito da contributi ad altri soggetti a 2,34 e competitività delle imprese a 2,14; il numero di enti resta a 0,96, cioè praticamente neutro">
  <figcaption>
    Gli otto fattori messi a confronto <strong>a parità di tutto il resto</strong>. Ogni pallino
    è un <em>odds ratio</em>: quante volte cambia il rapporto fra la probabilità di essere etichettato come "a rischio" e
    quella di non esserlo, rispetto a un progetto di riferimento: Centro-Nord, tema ambiente, intervento di acquisto beni, importo fra 100 e 500 mila euro. I trattini attorno sono il
    margine di incertezza. Il grafico completo, con
    tutti i fattori e le verifiche, è <a href="{{ site.baseurl }}/regressione.html#odds-ratio">nella
    pagina della regressione</a>.
  </figcaption>
</figure>


## Il parere dell'esperto

Dai dati di OpenCoesione è possibile estrarre le variabli che caratterizzano i progetti "a rischio", ma non i meccanismi che regolano le fasi di progettazione e sviluppo. 
**Giuseppe Magnifico**, dirigente dell'Ufficio Grant e Infrastrutture di Ricerca del CNR,
conosce da vicino i **meccanismi** del finanziamento pubblico: nella sua esperienza, **organici ridotti**, **competenze progettuali scarse** e uffici tecnici che devono gestire **pratiche complesse** sono il limite principale alla realizzazione puntuale dei progetti.

<!-- 🎙️ INTERVISTA (capacità amministrativa, Atto II) · citazione VERBATIM (sez. B di
     virgolettati_intervista.md). ⚠️ DA AUTORIZZARE e da verificare il nome. -->
<div class="quote-int">
  <p class="quote-int__label">Dall'intervista</p>
  <blockquote>
    «Qualsiasi attività di progettazione e ricerca non è soltanto una questione di ideazione: bisogna tenere in considerazione una
    serie di procedure contabili che devono essere gestite dal personale amministrativo, di cui abbiamo una grande carenza, non solo come CNR ma in generale come Paese.»
  </blockquote>
  <p class="quote-int__source"><strong>Giuseppe Magnifico</strong>, CNR · luglio 2026</p>
</div>

Sembra dunque evidente che il problema delle politiche di coesione non riguarda solo il tipo di progetto o la quantità di fondi erogati, ma anche l'intero corpo amministrativo che si ritrova a gestirli.  

## Il modello predittivo

A questo punto la domanda diventa un'altra: se sappiamo *che cosa* rende fragile un progetto,
riusciamo a **riconoscerlo in anticipo**? Abbiamo messo alla prova un secondo modello, un
[Random Forest]({{ site.baseurl }}/random-forest.html), che invece di misurare il peso isolato di
ogni fattore cerca da solo le combinazioni che portano al blocco. Prevede nettamente meglio della
regressione e, in combinazione con un metodo di spiegabilità come SHAP, permette di individuare le
caratteristiche del progetto da tenere d'occhio per anticipare il rischio. Il Random Forest conferma
quanto visto nella regressione: mette in cima ai fattori di rischio il territorio e l'erogazione di
contributi, e colloca l'acquisto di beni in fondo, pur sfruttando molto la fonte di finanziamento
per riconoscere l'origine dei progetti. 


# Cosa fare: il verdetto e una via d'uscita {#cosa-fare}

<figure style="margin: 1.5rem 0;">
  <img src="{{ site.baseurl }}/assets/images/hero_conclusions.jpg" alt="Svincolo autostradale visto dall'alto"
       style="width: 100%; border-radius: 4px;">
  <figcaption style="font-size: 0.8rem; color: #888; margin-top: 0.4rem;">
    I fondi arrivano a destinazione solo se il percorso non si interrompe.
  </figcaption>
</figure>

Misurata sul suo obiettivo dichiarato, l'equità territoriale, la politica di coesione **manca il
bersaglio proprio dove punta**: gli esiti sono sistematicamente peggiori nel Mezzogiorno, che dei
fondi è il primo destinatario.

Ma guardiamo al bicchiere mezzo pieno. Con più tempo a disposizione rispetto alla data di fine
prevista, molti progetti vengono comunque conclusi. Ci sono regioni che funzionano (la Liguria ha
solo il **9,2%** a rischio) e temi che viaggiano bene, come **energia** e **reti digitali** (rischio
sotto il 25%).

<!-- 🎙️ INTERVISTA (bicchiere, Atto III) · citazione VERBATIM (sez. C di virgolettati_intervista.md). -->
<!-- Stile unico dei virgolettati (25/07): era la variante pull quote con la virgoletta in
     filigrana, ora usa la stessa `.quote-int` delle altre due citazioni della pagina. -->
<div class="quote-int">
  <p class="quote-int__label">Dall'intervista</p>
  <blockquote>
    «Io personalmente vedo il bicchiere sempre pieno […]: ci sono moltissime eccellenze, ma il
    sistema non è solido come Paese, e quindi necessariamente ci sono gruppi più forti che vanno
    più avanti, e tendenzialmente sono nella parte del Centro-Nord su molte partite.»
  </blockquote>
  <p class="quote-int__source"><strong>Giuseppe Magnifico</strong>, CNR · luglio 2026</p>
  <p class="quote-int__note">Citazione in attesa di revisione finale dell'intervistato.</p>
</div>

<!-- ✅ Migrato al rischio il 25/07 (figura rigenerata dal nb 01 §7: prima era sui conclusi).
     ⚠️ Cambiando metrica cambiano anche le eccezioni al gradiente: non è più il solo Lazio. -->
<figure class="fig-home fig-home--narrow">
  <img src="{{ site.baseurl }}/assets/images/eda/08_regioni.png"
       alt="Classifica delle regioni per percentuale di progetti a rischio: Sicilia ultima con il 53,8%, Liguria prima con il 9,2%">
  <figcaption>
    Il bicchiere, regione per regione: in testa la Liguria (<strong>9,2%</strong> a rischio), in coda
    la Sicilia (<strong>53,8%</strong>). Il gradiente Nord–Sud ha però eccezioni in tutte e due le
    direzioni: le <strong>Marche</strong> (31,4%) e il <strong>Lazio</strong> (27,6%) stanno peggio
    di quattro regioni del Sud, e il <strong>Molise</strong> (16,5%) sta davanti a Lombardia,
    Piemonte e Veneto. La geografia non spiega tutto da sola.
  </figcaption>
</figure>

## E adesso? Due leve (e una parte che spetta a te)

La prima leva è la **formazione e il rafforzamento dei funzionari pubblici**, soprattutto nei
piccoli comuni del Mezzogiorno: concorsi, competenze tecniche, assistenza alla progettazione. Di
questo ci sono esempi virtuosi, come racconta Magnifico:

<!-- 🎙️ INTERVISTA (Bologna, CTA) · citazione VERBATIM (sez. D di virgolettati_intervista.md). -->
<div class="quote-int">
  <p class="quote-int__label">Dall'intervista</p>
  <blockquote>
    «L'Università di Bologna, qualche anno fa, ha cambiato il direttore generale; è arrivato un
    direttore proveniente dall'impresa, che ha chiamato a raccolta cinquanta persone capaci e ha
    creato un grosso gruppo che doveva dare supporto ai ricercatori e al personale […] per
    partecipare ai progetti europei.»
  </blockquote>
  <p class="quote-int__source"><strong>Giuseppe Magnifico</strong>, CNR · luglio 2026</p>
  <p class="quote-int__note">Citazione in attesa di revisione finale dell'intervistato.</p>
</div>

I risultati sono stati eccezionali, tanto che l'allora ministra dell'Istruzione, dell'Università e
della Ricerca Maria Chiara Carrozza ha intravisto in questo approccio un metodo da estendere anche
ad altri enti di ricerca.

La seconda leva è la **pressione sulle politiche locali**: i dati di OpenCoesione sono pubblici
proprio perché i cittadini possano chiedere conto dei progetti dei propri territori. **I soldi per
l'equità ci sono già: quello che manca si può costruire.**

<hr>

<p style="font-size: 0.8rem; color: #888; margin-top: 1.5rem;">
  Dati: <a href="https://opencoesione.gov.it" target="_blank" rel="noopener">OpenCoesione</a>,
  progetti ≥100.000 € pubblicati, snapshot al <strong>31 dicembre 2025</strong> (download del 6 maggio 2026).
  La data di riferimento di tutte le metriche («a rischio» inclusa) è la data dello snapshot.<br>
  Immagine di copertina: foto di <a href="https://unsplash.com/photos/zN4mtLHkHn4" target="_blank" rel="noopener">Fahrul Azmi</a> su <a href="https://unsplash.com" target="_blank" rel="noopener">Unsplash</a>.
  Svincolo aereo: foto di <a href="https://unsplash.com/photos/zBrnXi2IgpY" target="_blank" rel="noopener">Rodrigo Kugnharski</a>, Parco del Portello, Milano, su <a href="https://unsplash.com" target="_blank" rel="noopener">Unsplash</a>.
  Nave portacontainer (pagina Regressione): foto di <a href="https://unsplash.com/photos/1cqIcrWFQBI" target="_blank" rel="noopener">Venti Views</a> su <a href="https://unsplash.com" target="_blank" rel="noopener">Unsplash</a>.
  Bosco dall'alto (pagina Random Forest): foto di <a href="https://unsplash.com/photos/3BlVILvh9hM" target="_blank" rel="noopener">Olena Bohovyk</a> su <a href="https://unsplash.com" target="_blank" rel="noopener">Unsplash</a>.
  Spiaggia dall'alto (pagina Clustering): foto di <a href="https://unsplash.com/photos/jrBYlhSc5Lk" target="_blank" rel="noopener">Alessandro Brunello</a> su <a href="https://unsplash.com" target="_blank" rel="noopener">Unsplash</a>.
  Archivio (pagina Text Analysis): foto di <a href="https://unsplash.com/photos/MguscIwbBjU" target="_blank" rel="noopener">Studio Crevettes</a> su <a href="https://unsplash.com" target="_blank" rel="noopener">Unsplash</a>.<br>
  Immagine di anteprima (thumbnail): ID <a href="https://www.dreamstime.com/royalty-free-stock-image-italy-euro-image22014316" target="_blank" rel="noopener">22014316</a> © <a href="https://www.dreamstime.com/zimmytws_info" target="_blank" rel="noopener">Zimmytws</a> | <a href="https://www.dreamstime.com/" target="_blank" rel="noopener">Dreamstime.com</a>.
</p>
