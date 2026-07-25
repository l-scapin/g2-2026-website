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

# Che cos'è la politica di coesione (e perché ti riguarda) {#coesione}

**Che cosa.** Le politiche di coesione sono lo strumento con cui l'Unione Europea e lo Stato
italiano finanziano interventi per ridurre i divari tra territori: infrastrutture, ricerca,
ambiente, scuole, servizi. **Chi paga**: fondi europei più un consistente cofinanziamento
nazionale (il solo Fondo Sviluppo e Coesione vale circa 99 miliardi). In entrambi i casi la
fonte ultima è la stessa: le tasse di tutti. **Quanto**: nei progetti monitorati da
**OpenCoesione** (il portale pubblico che li documenta uno per uno) passano oltre **315
miliardi di euro** di finanziamento pubblico (qui fotografati al **31 dicembre 2025**).
**Dove e quando**: in tutta Italia, per cicli di programmazione di sette anni (dal 2000-2006 al
2021-2027), con più risorse al Mezzogiorno, coerentemente con la missione redistributiva.
**Perché**: l'obiettivo dichiarato è l'**equità territoriale**, che nascere a Enna o a Bolzano non
determini la qualità dei servizi a cui hai accesso. Noi analizziamo i progetti da almeno 100.000 €
con i metodi statistici documentati nelle pagine tecniche del menu «Le analisi»:
[esplorazione dei dati]({{ site.baseurl }}/eda.html), [clustering]({{ site.baseurl }}/clustering.html),
[regressione]({{ site.baseurl }}/regressione.html), [Random Forest]({{ site.baseurl }}/random-forest.html).

<!-- GRAFICO · Sankey (versione leggera, la stessa dell'EDA). Spostato qui il 24/07: chiude la
     sezione "Che cos'è" visualizzando il flusso dei 315 mld da fonte a territorio a tema, cioè
     esattamente il "Chi paga / Quanto" appena descritto. -->

<figure class="fig-home">
  <iframe src="{{ site.baseurl }}/assets/charts/plotly/sankey_fondi.html"
          title="Diagramma di Sankey: il percorso dei fondi dalla fonte al territorio al tema"
          style="width: 100%; height: 520px; border: none;"
          loading="lazy"></iframe>
  <figcaption>
    Il percorso dei 315 miliardi: da ogni <strong>fonte</strong>, europea o nazionale (FSC, PAC,
    rotazione), al <strong>territorio</strong>, fino al <strong>tema</strong>. Lo spessore dei flussi
    è proporzionale ai fondi pubblici. Due letture: al Sud la coesione è più nazionale (FSC) che
    europea, e i trasporti assorbono la fetta maggiore. Passa il mouse sui flussi per i valori;
    la legenda completa delle fonti è <a href="{{ site.baseurl }}/eda.html#dove-passano-i-fondi">nell'EDA</a>.
  </figcaption>
</figure>

<!-- GRAFICO · bilanciamento del dataset (nb 01 §3, stesso file usato dall'EDA). Sta qui, subito
     sotto il Sankey: il Sankey mostra che i FONDI sono sbilanciati verso il Sud, questo mostra che
     i PROGETTI no, e prepara il confronto in percentuale del paragrafo successivo. -->

<figure class="fig-home">
  <img src="{{ site.baseurl }}/assets/images/eda/04b_bilanciamento.png"
       alt="Barra divisa in due: il 44,0% dei progetti sta nel Centro-Nord e il 56,0% nel Mezzogiorno, quindi vicino alla metà esatta">
  <figcaption>
    Quanti progetti stanno da una parte e dall'altra: dei <strong>204.060</strong> progetti
    localizzati in una delle due aree, il <strong>44,0%</strong> è nel Centro-Nord (89.831) e il
    <strong>56,0%</strong> nel Mezzogiorno (114.229). Serve a leggere tutto quello che viene dopo:
    i due gruppi sono di taglia simile, quindi il divario del prossimo capitolo non è l'effetto di
    quanti progetti ci sono da una parte e dall'altra. I <strong>soldi</strong>, invece, sono
    sbilanciati, e si vede nel diagramma qui sopra: <strong>73% al Sud contro 27%</strong>.
  </figcaption>
</figure>

# Il problema: i progetti si fermano dove servono di più {#il-problema}

Dei 206.777 progetti, il **48,9%** si è concluso, mentre il **32,6%** è **a rischio**. Al
Centro-Nord il rischio tocca il **20,5%** dei progetti; nel Mezzogiorno il **42,0%**: **il doppio**.
Eppure il Sud gestisce **215 miliardi** contro i 79 del Centro-Nord: i soldi ci sono, è il percorso
che si interrompe.

<!-- BOX DEFINIZIONE · "a rischio" è la nostra variabile chiave e la definiamo noi. -->
<div class="def-box">
  <p class="def-box__label">La nostra variabile chiave</p>
  <h4>Quando un progetto è «a rischio»?</h4>
  <p>In mancanza di un'etichetta ufficiale, abbiamo deciso di calcolare il rischio partendo da due
  segnali osservabili nei dati alla data di riferimento, il <strong>31 dicembre 2025</strong>, la data
  a cui è aggiornato il dataset. Un progetto è «a rischio» se:</p>
  <p><strong>1 · non è mai partito</strong>: risulta ancora «non avviato»
  (16.261 progetti, il 7,9%), <em>oppure</em><br>
  <strong>2 · è fuori tempo massimo</strong>: è «in corso» ma la sua data di fine prevista
  è già passata (51.237 progetti, il 24,8%).</p>
  <p>In totale abbiamo etichettato come a rischio <strong>67.498 progetti, il 32,6%</strong> del
  totale. Ma «a rischio» non significa fallito: significa che il percorso si è inceppato e l'esito
  è in dubbio.</p>
  <p class="def-box__note">Nota di trasparenza: la definizione non riguarda i progetti <em>conclusi</em>
  in ritardo, ma quelli ancora in corso oltre la data di scadenza. Ed è la fotografia di un istante:
  un progetto oggi a rischio può ancora arrivare in fondo.</p>
</div>

Le cifre con cui abbiamo a che fare sono enormi: nei progetti a rischio sono impegnati
**122,5 miliardi di euro** di finanziamento pubblico (più di un terzo dell'intero portafoglio),
di cui risultano pagati finora solo 45,5. Ci sono **26,3 miliardi** fermi in 16.261 progetti
**mai avviati**, con zero pagamenti. E la geografia del denaro fermo ricalca quella del bisogno:
**99,4 miliardi a rischio nel Mezzogiorno**, 18,5 nel Centro-Nord.

<!-- GRAFICO · Mappa del rischio (statica, dall'EDA). -->

<figure class="fig-home fig-home--narrow">
  <img src="{{ site.baseurl }}/assets/images/eda/mappa_rischio.png"
       alt="Mappa dell'Italia: percentuale di progetti a rischio per regione, con gradiente che cresce da Nord a Sud">
  <figcaption>
    La geografia del rischio: quota di progetti a rischio per regione. Il colore si scurisce
    scendendo lungo la penisola, fino alla Sicilia che supera il 50%. La versione interattiva,
    con classifica regionale e la scelta fra rischio totale, progetti mai avviati e progetti fuori
    tempo massimo, è <a href="{{ site.baseurl }}/eda.html#la-mappa-regionale">nell'EDA</a>.
  </figcaption>
</figure>

Perché dovrebbe importarti? Perché quei miliardi sono **i tuoi**: tasse italiane ed europee. E
perché dietro ogni progetto fermo c'è un pezzo di diritti di qualcuno: l'asilo non aperto, la
ferrovia non ammodernata, il depuratore non finito. Quando un progetto si ferma al Sud, l'obiettivo
dell'equità territoriale (la ragione per cui quei fondi esistono) si allontana sempre di più.

# Perché succede: l'identikit del rischio {#perche-succede}

Se il problema fosse casuale, colpirebbe a caso. Invece ha un identikit preciso.

**Dimensione.** Il rischio cresce con la quantità di fondi stanziati per ciascun progetto: il punto
critico sono i progetti **medio-grandi**, quelli fra 5 e 10 milioni, a rischio nel **43,9%** dei
casi contro il 29,4% dei più piccoli. Sopra i 50 milioni scende al 38,5%, e restano comunque 623
progetti che da soli valgono 120,5 miliardi: pochi e pesantissimi.

**Ciclo.** Il ciclo di finanziamenti riserva la sorpresa più grande. Il più impantanato non è
quello appena partito ma il **2014-2020, a rischio al 38,5%**, sopra il 2021-2027 che si ferma al
36,8% pur avendo davanti ancora tutta la corsa.

**Tema.** Alcuni temi risultano più a rischio di altri: la **competitività delle imprese** (39,6%),
i **trasporti** (37,2%) e l'**ambiente** (34,9%). E soprattutto il rischio cresce **a Sud**, dentro
ogni ciclo di programmazione: il divario Centro-Nord/Mezzogiorno nel rischio è **persistente**, non
l'effetto di una stagione sfortunata.

<!-- GRAFICI · dimensione (campana) e persistenza del divario per ciclo. -->

<figure class="fig-home">
  <img src="{{ site.baseurl }}/assets/images/eda/05_dimensione_rischio.png"
       alt="Grafico a barre: la percentuale di progetti a rischio sale fino al 43,9% nella fascia 5-10 milioni e poi ridiscende">
  <figcaption>
    Il rischio non cresce all'infinito con la taglia: disegna una campana. Dal 29,4% dei progetti
    piccoli (100–500k €) sale al <strong>43,9% della fascia 5-10 milioni</strong>, poi ridiscende
    al 38,5% sopra i 50 milioni. Il punto debole sono i progetti medio-grandi.
  </figcaption>
</figure>

<!-- ✅ Migrato al rischio il 25/07 (figura rigenerata dal nb 01 §3.1: prima era sui conclusi). -->
<figure class="fig-home">
  <img src="{{ site.baseurl }}/assets/images/eda/07_divario_per_ciclo.png"
       alt="Barre appaiate Centro-Nord e Mezzogiorno: in ogni ciclo di programmazione il Mezzogiorno ha una quota maggiore di progetti a rischio">
  <figcaption>
    Il divario non è l'incidente di una stagione: <strong>dentro ogni ciclo</strong> il Mezzogiorno
    ha più progetti a rischio del Centro-Nord (+28,4, +21,1, +30,0 e +12,3 punti, dal 2000-06 al
    2021-27 appena partito).
  </figcaption>
</figure>

Verrebbe da pensare che i progetti con più soggetti coinvolti
(più enti, più tavoli, più firme) siano i più fragili. I dati dicono di no: la correlazione
tra numero di enti e rischio è praticamente nulla, e i progetti con più di 5 enti sono anzi i
*meno* a rischio. L'apparente eccezione (un picco di rischio nei progetti con 3 enti) svanisce
guardando da vicino: è quasi tutta concentrata in pochi programmi del ciclo 2007-2013, in
Sicilia e Calabria.

I dati OpenCoesione dicono *dove* e *quanto* i progetti si fermano, non *chi* o *che cosa* li
ferma. Giuseppe Magnifico, dirigente dell'Ufficio Grant e Infrastrutture di Ricerca del CNR,
conosce da vicino i meccanismi del finanziamento pubblico: nella sua esperienza, organici ridotti,
competenze progettuali scarse e uffici tecnici che devono gestire pratiche complesse senza le
persone per farlo sono il limite principale alla realizzazione puntuale dei progetti.

<!-- 🎙️ INTERVISTA (capacità amministrativa, Atto II) · citazione VERBATIM (sez. B di
     virgolettati_intervista.md). ⚠️ DA AUTORIZZARE e da verificare il nome. -->
<div class="quote-int">
  <p class="quote-int__label">Dall'intervista</p>
  <blockquote>
    «Qualsiasi attività di ricerca non è soltanto ideazione e articolo pubblicato: c'è tutta una
    serie di procedure contabili che devono essere gestite dal personale amministrativo, e di questo
    noi abbiamo una grande carenza, come CNR ma in generale come Paese. Siamo molto più in basso
    rispetto alla Spagna o alla Francia.»
  </blockquote>
  <p class="quote-int__source"><strong>Giuseppe Magnifico</strong>, CNR · luglio 2026</p>
  <p class="quote-int__note">Citazione in attesa di revisione finale dell'intervistato.</p>
</div>

Se è così, chi più avrebbe bisogno dei fondi, meno ha gli strumenti per spenderli. I fondi possono
comprare cemento e servizi, ma non possono comprare da soli la macchina amministrativa che serve a
spenderli.

<!-- ✅ MODELLO: regressione estesa del Notebook 02, OR Mezzogiorno 2,80 [2,74–2,86]; contributi ad
     altri 2,34 · lavori pubblici 1,81 · quota UE 0,78 · capitale privato 0,68 · NUM_ENTI 0,96. -->
Per capire il ruolo del territorio in questa dinamica ci vengono incontro i risultati del
**modello multivariato** (pagina [regressione]({{ site.baseurl }}/regressione.html)), che mette
tutti i fattori sullo stesso piano, confrontando progetti **a parità di** tipo di intervento, tema,
dimensione e fonte di finanziamento. Stando al modello, a parità di tutto il resto, per un progetto
del Mezzogiorno il rapporto tra la probabilità di incepparsi e quella di non incepparsi è **quasi il
triplo** che al Centro-Nord (odds ratio **2,80**, IC 95% 2,74–2,86) e, specularmente, concludere è
molto meno probabile. Rifacendo il conto **dentro ogni ciclo di programmazione**, uno alla volta, il
divario non sparisce mai: enorme nei cicli ormai chiusi, più contenuto nel 2021-2027 partito da
poco, ma sempre lì. Nei due cicli centrali, quelli con più progetti, vale addirittura **quasi
quattro volte**.

Il modello mette anche in evidenza il peso del progetto. Rispetto a un intervento
che si limita ad acquistare beni, erogare contributi ad altri soggetti moltiplica per **2,3** le
odds di finire a rischio, e realizzare lavori pubblici per **1,8**. Costruire un'opera, o passare i
soldi a qualcun altro perché li spenda, è un fattore di rischio più grande rispetto ai progetti che
prevedono acquisti, ed è una leva su cui, a differenza della geografia, si può agire scrivendo
diversamente i bandi. Inoltre i progetti
finanziati con **fondi europei**, a prescindere dalla quantità del finanziamento, sono meno a
rischio e concludono di più, a parità di tutto il resto: arrivano con scadenze vincolanti e regole
di disimpegno. E il confine è netto più che graduale, quello che conta è **avere** fondi europei,
non quanti: che la quota europea sia un quinto o quasi tutto il finanziamento cambia poco, a fare la
differenza sono le regole del canale, non la percentuale. Vale qualcosa di simile per il **capitale
privato**, ma solo dove il privato cofinanzia il proprio investimento: negli incentivi alle imprese
chi mette dei soldi propri è a rischio nel 31,8% dei casi contro il 36,6%, mentre altrove la
differenza sparisce.

<!-- GRAFICO · forest plot divulgativo (make_mod_landing_or.py). -->

<figure class="fig-home">
  <img src="{{ site.baseurl }}/assets/images/modello/mod_landing_or.png"
       alt="Grafico a pallini con intervalli di confidenza: il Mezzogiorno è il fattore più forte a 2,80, seguito da contributi ad altri soggetti a 2,34 e competitività delle imprese a 2,14; il numero di enti resta a 0,96, cioè praticamente neutro">
  <figcaption>
    Gli otto fattori messi a confronto <strong>a parità di tutto il resto</strong>. Ogni pallino
    è un <em>odds ratio</em>: quante volte cambia il rapporto fra la probabilità di incepparsi e
    quella di non incepparsi, rispetto a un progetto di riferimento. I trattini attorno sono il
    margine di incertezza. Il grafico completo, con
    tutti i fattori e le verifiche, è <a href="{{ site.baseurl }}/regressione.html#odds-ratio">nella
    pagina della regressione</a>.
  </figcaption>
</figure>

<!-- ✅ RANDOM FOREST · AUC 0,813 sul test contro 0,669 della logistica; SHAP conferma l'ordine. -->
A questo punto la domanda diventa un'altra: se sappiamo *che cosa* rende fragile un progetto,
riusciamo a **riconoscerlo in anticipo**? Abbiamo messo alla prova un secondo modello, un
[Random Forest]({{ site.baseurl }}/random-forest.html), che invece di misurare il peso isolato di
ogni fattore cerca da solo le combinazioni che portano al blocco. Prevede nettamente meglio della
regressione e, in combinazione con un metodo di spiegabilità come SHAP, permette di individuare le
caratteristiche del progetto da tenere d'occhio per anticipare il rischio. Il Random Forest conferma
quanto visto nella regressione: mette in cima ai fattori di rischio il territorio e l'erogazione di
contributi, e colloca l'acquisto di beni in fondo, pur sfruttando molto la fonte di finanziamento
per riconoscere l'origine dei progetti. Due modelli costruiti su logiche diverse arrivano così alle
stesse conclusioni.


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
