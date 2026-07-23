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
     Articolo in 3 atti. Stato al 22/07/2026: NON ci sono più slot vuoti in pagina. I due box in
     attesa (dato ISTAT e citazione da fonte pubblicata) sono stati rimossi il 22/07 per decisione
     di Ale: si consegna con il materiale che abbiamo. Restano da fare solo clustering e text
     analysis, che vivono sulle loro pagine e non aprono buchi qui.
     🎙️ INTERVISTA = quattro box con citazioni VERBATIM, MAI virgolettati inventati.
                     L'intervistato ("Magnifico") si occupa di PNRR e fondi nazionali: le sue
                     parole vanno CONTESTUALIZZATE (esperienza di gestione di fondi pubblici),
                     non spacciate per testimonianza sui fondi di coesione, che sono un canale
                     diverso. ⚠️ Tutte da autorizzare prima della consegna.
     TODO scrollytelling: il tema ha scrollama (vedi demo): da valutare sugli atti in seconda battuta.
     Tutti i numeri sono stati RICALCOLATI il 17/07/2026 con la data di riferimento corretta
     (31/12/2025 = snapshot del dataset; prima era 06/05/2025 per refuso). Non arrotondare 32,6 → 32.
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

Un progetto su due è arrivato a conclusione, e i cicli più recenti sono ancora in corsa. Ma
dietro la media c'è una spaccatura: al Centro-Nord si chiude quasi il **59%** dei progetti, al Sud
il **42%**, eppure è il Mezzogiorno a gestire più fondi. E non è l'incidente di un anno storto:
il divario **resiste dentro ogni ciclo** di programmazione. Questa è la storia di dove i soldi
si fermano, e di che cosa si inceppa.
{: .lead }

# Che cos'è la politica di coesione (e perché ti riguarda) {#coesione}

**Che cosa.** La politica di coesione è lo strumento con cui l'Unione Europea e lo Stato
finanziano interventi per ridurre i divari tra territori: infrastrutture, ricerca, ambiente,
scuole, servizi. **Chi paga**: fondi europei (FESR, FSE) più un consistente cofinanziamento
nazionale (il solo Fondo Sviluppo e Coesione vale circa 99 miliardi). In entrambi i casi la
fonte ultima è la stessa: le tasse di tutti. **Quanto**: nei progetti monitorati da
**OpenCoesione** (il portale pubblico che li documenta uno per uno) passano oltre **315
miliardi di euro** di finanziamento pubblico (qui fotografati al **31 dicembre 2025**). **Dove e quando**: in tutta Italia, per cicli di
programmazione di sette anni (dal 2000-2006 al 2021-2027), con più risorse al Mezzogiorno,
coerentemente con la missione redistributiva. **Perché**: l'obiettivo dichiarato è l'**equità
territoriale**: che nascere a Enna o a Bolzano non determini la qualità dei servizi a cui hai
accesso. Noi analizziamo i progetti da almeno 100.000 € (il PNRR è un canale diverso e resta
fuori) con i metodi statistici documentati nelle pagine tecniche del menu «Le analisi»:
[esplorazione dei dati]({{ site.baseurl }}/eda.html), [regressione]({{ site.baseurl }}/regressione.html),
[Random Forest]({{ site.baseurl }}/random-forest.html).

<!-- Qui c'era il box CONTESTO INEGUAGLIANZA, in attesa di un dato ISTAT sul divario territoriale
     (popolazione del Mezzogiorno, migrazione dei laureati, asili nido). Rimosso il 22/07/2026:
     si consegna con i dati che abbiamo. Se qualcuno lo recupera, va verificato alla fonte prima
     di scriverlo. -->
<!-- 🎙️ INTERVISTA (frase breve): riempito il 16/07/2026 con citazione VERBATIM dalla
     trascrizione (Data Journalism e struttura/Intervista_esperto_CNR_fondi_coesione.docx;
     selezione completa in virgolettati_intervista.md). ⚠️ DA AUTORIZZARE: l'intervistato ha
     chiesto di rivedere il lavoro prima della consegna. Decidere col gruppo: nome esplicito o
     "dirigente CNR". Contesto dichiarato nel testo: la sua esperienza è PNRR/fondi nazionali,
     non coesione. Stessa voce chiude l'articolo nell'Atto III. -->
<div style="border-left: 4px solid #177E89; padding: 0.6rem 0 0.6rem 1.2rem; margin: 2.2rem 0;">
  <p style="font-size: 1.15rem; color: #2b2b2b; margin-bottom: 0.5rem;">
    🎙️ «Io ho sì la data d'inizio, ma non posso avere la persona reclutata per quella data.»
  </p>
  <p style="font-size: 0.95rem; color: #2b2b2b; margin-bottom: 0.5rem;">
    A raccontarci come un progetto pubblico possa restare al palo prima ancora di partire
    (con le persone chiave che arrivano, «se tutto va bene», sei mesi o un anno dopo l'avvio
    formale) è un dirigente del CNR con esperienza diretta nella gestione di fondi pubblici
    (PNRR e fondi nazionali: un canale diverso dalla coesione, ma la stessa macchina
    amministrativa). La sua lettura completa chiude questo articolo.
  </p>
  <p style="font-size: 0.82rem; color: #888; margin: 0;">
    Dalla trascrizione dell'intervista, luglio 2026 · citazioni in attesa di revisione finale dell'intervistato
  </p>
</div>

# Il problema: i progetti si fermano dove servono di più {#il-problema}

<!-- ATTO I · inciting event. BOZZA: prosa da rifinire, numeri già verificati. -->

Il protagonista di questa storia non è una persona: sono i **fondi di coesione**, 315 miliardi
di euro con una missione scritta nei trattati: riequilibrare i territori. Il loro oggetto del
desiderio è l'**equità territoriale**. E come in ogni storia, a un certo punto qualcosa si
inceppa: **non tutti i progetti si concludono, e falliscono più spesso proprio dove servirebbero
di più**.

I numeri dell'inciampo, alla data di riferimento (31 dicembre 2025): dei 206.777 progetti,
è concluso il **48,9%**, mentre il **32,6%** è **a rischio**. Al Centro-Nord il rischio tocca il
**20,5%** dei progetti; nel Mezzogiorno il **42,0%**: **il doppio**. Eppure il Sud gestisce
**215 miliardi** contro i 79 del Centro-Nord: i soldi ci sono, è il percorso che si interrompe.

<!-- BOX DEFINIZIONE · "a rischio" è la nostra variabile chiave e la definiamo noi:
     va dichiarata in modo inequivocabile. Numeri verificati sul dataset (15/07/2026). -->
<div class="def-box">
  <p class="def-box__label">La nostra variabile chiave</p>
  <h4>Quando un progetto è «a rischio»?</h4>
  <p>Non esiste un'etichetta ufficiale: <strong>l'abbiamo costruita noi</strong>, da due segnali
  osservabili nei dati alla data di riferimento: il <strong>31 dicembre 2025</strong>, la data
  a cui è aggiornato il dataset. Un progetto è «a rischio» se:</p>
  <p><strong>1 · non è mai partito</strong>: risulta ancora «non avviato»
  (16.261 progetti, il 7,9%), <em>oppure</em><br>
  <strong>2 · è fuori tempo massimo</strong>: è «in corso» ma la sua data di fine prevista
  è già passata (51.237 progetti, il 24,8%).</p>
  <p>In totale: <strong>67.498 progetti, il 32,6%</strong>. «A rischio» non significa fallito:
  significa che il percorso si è inceppato e l'esito è in dubbio.</p>
  <p class="def-box__note">Nota di trasparenza: un progetto <em>concluso</em> in ritardo non conta
  come a rischio: la definizione guarda chi è ancora per strada, non chi è arrivato tardi. Ed è la
  fotografia di un istante: un progetto oggi a rischio può ancora arrivare in fondo.</p>
</div>

<!-- GRAFICO · Sankey (versione leggera, esatta all'euro, la stessa dell'EDA).
     Risponde letteralmente al titolo del sito: da dove arrivano i soldi e dove vanno.
     La legenda completa dei fondi resta nell'EDA: qui solo la lettura essenziale. -->

<figure class="fig-home">
  <iframe src="{{ site.baseurl }}/assets/charts/plotly/sankey_fondi.html"
          title="Diagramma di Sankey: il percorso dei fondi dalla fonte al territorio al tema"
          style="width: 100%; height: 520px; border: none;"
          loading="lazy"></iframe>
  <figcaption>
    Il percorso dei 315 miliardi, esatto all'euro: da ogni <strong>fonte</strong>, europea (FESR, FSE)
    o nazionale (FSC, PAC, rotazione), al <strong>territorio</strong>, fino al <strong>tema</strong>. Lo spessore dei
    flussi è proporzionale ai fondi pubblici. Due letture: al Sud la coesione è più nazionale (FSC)
    che europea, e i trasporti assorbono la fetta maggiore. Passa il mouse sui flussi per i valori;
    la legenda completa delle fonti è <a href="{{ site.baseurl }}/eda.html#dove-passano-i-fondi">nell'EDA</a>.
  </figcaption>
</figure>

E parliamo di cifre che si fanno fatica a immaginare: nei progetti a rischio sono impegnati
**122,5 miliardi di euro** di finanziamento pubblico (più di un terzo dell'intero portafoglio),
di cui risultano pagati finora solo 45,5. Ci sono **26,3 miliardi** fermi in 16.261 progetti
**mai avviati**, con zero pagamenti. E la geografia del denaro fermo ricalca quella del bisogno:
**99,4 miliardi a rischio nel Mezzogiorno**, 18,5 nel Centro-Nord.

<!-- GRAFICO · Mappa del rischio (statica, dall'EDA, era il candidato indicato per l'Atto I).
     È l'immagine-chiave dell'atto: "si fermano dove servono di più" reso geografia. -->

<figure class="fig-home fig-home--narrow">
  <img src="{{ site.baseurl }}/assets/images/eda/mappa_rischio.png"
       alt="Mappa dell'Italia: percentuale di progetti a rischio per regione, con gradiente che cresce da Nord a Sud">
  <figcaption>
    La geografia del rischio: quota di progetti a rischio per regione. Il colore si scurisce
    scendendo lungo la penisola, fino alla Sicilia che supera il 50%. La versione interattiva,
    con classifica regionale e scelta della metrica, è <a href="{{ site.baseurl }}/eda.html#la-mappa-regionale">nell'EDA</a>.
  </figcaption>
</figure>

Perché dovrebbe importarti? Perché quei miliardi sono **i tuoi**: tasse italiane ed europee,
più il cofinanziamento nazionale. E perché dietro ogni progetto fermo c'è un pezzo di diritti
di qualcuno: l'asilo non aperto, la ferrovia non ammodernata, il depuratore non finito. Quando
un progetto si ferma al Sud, l'equità territoriale (la ragione per cui quei fondi esistono)
si allontana esattamente dove era più urgente.

# Perché succede: l'identikit del rischio (e un falso colpevole) {#perche-succede}

<!-- ATTO II · effetti + antagonista. BOZZA: prosa da rifinire, numeri verificati il 12-14/07. -->

Se il problema fosse casuale, colpirebbe a caso. Invece ha un identikit preciso. Il rischio
cresce con la **dimensione**, ma non all'infinito: il punto critico sono i progetti
**medio-grandi**, quelli fra 5 e 10 milioni, a rischio nel **43,9%** dei casi contro il 29,4% dei
più piccoli. Sopra i 50 milioni scende al 38,5%, e restano comunque 623 progetti che da soli
valgono 120,5 miliardi: pochi e pesantissimi. Il **ciclo** riserva la sorpresa più grande. Il più
impantanato non è quello appena partito ma il **2014-2020, a rischio al 38,5%**, sopra il
2021-2027 che si ferma al 36,8% pur avendo davanti ancora tutta la corsa. Cambia con il **tema**: in testa la **competitività delle
imprese** (39,6% a rischio, ed è anche il tema con meno progetti conclusi), poi **trasporti**
(37,2%) e **ambiente** (34,9%), mentre welfare e istruzione, contrariamente a quanto si
potrebbe pensare, restano attorno alla media, lontani dalla testa della classifica. E soprattutto cresce **a Sud**, dentro ogni ciclo
di programmazione: il divario Centro-Nord/Mezzogiorno nei conclusi è **persistente**, non
l'effetto di una stagione sfortunata.

<!-- GRAFICI · i due tratti più netti dell'identikit: dimensione e persistenza del divario.
     Il tema resta solo nel testo (il grafico per tema è nell'EDA): tre figure di fila
     appesantirebbero l'atto. -->

<figure class="fig-home">
  <img src="{{ site.baseurl }}/assets/images/eda/05_dimensione_rischio.png"
       alt="Grafico a barre: la percentuale di progetti a rischio sale fino al 43,9% nella fascia 5-10 milioni e poi ridiscende">
  <figcaption>
    Il rischio non cresce all'infinito con la taglia: disegna una campana. Dal 29,4% dei progetti
    piccoli (100–500k €) sale al <strong>43,9% della fascia 5-10 milioni</strong>, poi ridiscende
    al 38,5% sopra i 50 milioni. Il punto debole sono i progetti medio-grandi.
  </figcaption>
</figure>

<figure class="fig-home">
  <img src="{{ site.baseurl }}/assets/images/eda/07_divario_per_ciclo.png"
       alt="Barre appaiate Centro-Nord e Mezzogiorno: in ogni ciclo di programmazione il Centro-Nord conclude di più">
  <figcaption>
    Il divario non è l'incidente di una stagione: <strong>dentro ogni ciclo</strong> il Centro-Nord
    conclude più del Mezzogiorno (+30,6, +24,6, +37,5 e +5,5 punti, dal 2000-06 al 2021-27 appena partito).
  </figcaption>
</figure>

C'è anche un **falso colpevole**. Verrebbe da pensare che i progetti con più soggetti coinvolti
(più enti, più tavoli, più firme) siano i più fragili. I dati dicono di no: la correlazione
tra numero di enti e rischio è praticamente nulla, e i progetti con più di 5 enti sono anzi i
*meno* a rischio. L'apparente eccezione (un picco di rischio nei progetti con 3 enti) svanisce
guardando da vicino: è quasi tutta concentrata in pochi programmi del ciclo 2007-2013, in
Sicilia e Calabria. Anche il falso colpevole, insomma, riporta al territorio.

E qui entra in scena l'**antagonista**, che non abita nel dataset. I dati OpenCoesione dicono
*dove* e *quanto* i progetti si fermano, non *chi* o *che cosa* li ferma. L'ipotesi più
accreditata in letteratura è la **capacità amministrativa**: organici ridotti, competenze
progettuali scarse, uffici tecnici che devono gestire pratiche complesse senza le persone per
farlo. Se è così, il paradosso è crudele: **chi più avrebbe bisogno dei fondi, meno ha gli
strumenti per spenderli**. I fondi possono comprare cemento e servizi, ma non possono comprare
da soli la macchina amministrativa che serve a spenderli.

<!-- 🎙️ INTERVISTA (terza occorrenza, Atto II): citazione VERBATIM dalla trascrizione,
     sezione C di virgolettati_intervista.md. È la sua UNICA spiegazione esplicita del divario
     Nord/Sud oltre al "bicchiere" citato nell'Atto III, e aggiunge un meccanismo che i dati non
     vedono (la rete, non solo l'organico). ⚠️ Stesso caveat: esperienza PNRR/fondi nazionali,
     dichiarato nel testo. DA AUTORIZZARE con le altre. -->
<div style="border-left: 4px solid #177E89; padding: 0.6rem 0 0.6rem 1.2rem; margin: 2.2rem 0;">
  <p style="font-size: 1.05rem; color: #2b2b2b; margin-bottom: 0.5rem;">
    🎙️ «Pur avendo ottimi risultati, le regioni del Sud riescono di meno, se prendiamo ad esempio
    le progettualità di carattere europeo, perché non c'è una sufficiente massa critica in termini
    di network.»
  </p>
  <p style="font-size: 0.95rem; color: #2b2b2b; margin-bottom: 0.5rem;">
    Il dirigente del CNR che apre questo articolo aggiunge un secondo meccanismo accanto agli
    uffici sotto organico: le <strong>reti</strong>. Enti, imprese e università che non riescono a
    fare squadra abbastanza a lungo da reggere i progetti più ambiziosi. Un'ipotesi che il nostro
    dataset non può né confermare né smentire, perché registra i progetti finanziati, non quelli
    che nessuno è riuscito a mettere insieme.
  </p>
  <p style="font-size: 0.82rem; color: #888; margin: 0;">
    Dalla trascrizione dell'intervista, luglio 2026 · citazioni in attesa di revisione finale dell'intervistato
  </p>
</div>

<!-- Qui c'era lo SLOT FONTI ANTAGONISTA, cioè un box in attesa di una citazione da Corte dei
     Conti / SVIMEZ / Banca d'Italia. Rimosso il 22/07/2026: si consegna con quello che abbiamo.
     L'ipotesi della capacità amministrativa resta dichiarata come ipotesi nel paragrafo sopra e
     poggia sulla testimonianza dell'intervistato, non su letteratura. Se il gruppo trova il
     passaggio referenziato, va inserito qui, tra virgolette, con fonte e anno esatti. -->
<!-- ✅ MODELLO: aggiornato con la regressione estesa del Notebook 02 (sm.Logit su 206.757
     progetti, 25 parametri): OR Mezzogiorno 2,789 [2,731–2,849]; natura dell'intervento
     (rif. acquisto beni) contributi ad altri 2,34 · lavori pubblici 1,81 · incentivi 1,54 ·
     servizi 1,25; quota fondi UE 0,783; quota capitale privato 0,681 (effetto concentrato sugli
     incentivi); NUM_ENTI 0,957; stima dentro ogni ciclo: 17,3 / 3,84 / 3,72 / 1,42;
     AUC 0,668, test 0,665. PROSA DA RIFINIRE COL GRUPPO. -->
Ma il territorio conta *di per sé*, o è solo il riflesso di come sono fatti i progetti che
ospita? Il **modello multivariato** (pagina [regressione]({{ site.baseurl }}/regressione.html)) mette
tutti i fattori sullo stesso piano, confrontando progetti **a parità di** tipo di intervento,
tema, dimensione e fonte di finanziamento. Il verdetto: **il divario non si spiega con la
composizione dei portafogli**. A parità di tutto il resto, per un progetto del Mezzogiorno il
rapporto tra la probabilità di incepparsi e quella di non incepparsi è **quasi il triplo** che
al Centro-Nord (odds ratio **2,80**, IC 95% 2,74–2,86) e, specularmente, concludere è molto
meno probabile. Rifacendo il conto **dentro ogni ciclo di programmazione**, uno alla volta, il
divario non sparisce mai: enorme nei cicli ormai chiusi, più contenuto nel 2021-2027 appena
partito, ma sempre lì. Nei due cicli centrali, quelli con più progetti e più storia, vale
addirittura **quasi quattro volte**.

Il modello aggiunge però una cosa che l'esplorazione non aveva visto: **conta moltissimo che
cosa il progetto fa**. Rispetto a un intervento che si limita ad acquistare beni, erogare
contributi ad altri soggetti moltiplica per **2,3** le odds di finire a rischio, e realizzare
lavori pubblici per **1,8**. Costruire un'opera, o passare i soldi a qualcun altro perché li
spenda, è molto più fragile che comprare, ed è una leva su cui, a differenza della geografia,
si può agire scrivendo diversamente i bandi. Nella stessa direzione va un secondo risultato: i
progetti finanziati con **fondi europei** sono meno a rischio e concludono di più, a parità di
tutto il resto. Sono anche quelli che arrivano con scadenze vincolanti e regole di disimpegno.
E il confine è netto più che graduale: quello che conta è **avere** fondi europei, non quanti.
Una volta che il progetto è dentro quel canale, che la quota europea sia un quinto o quasi tutto
il finanziamento cambia poco: a cambiare le cose sono le regole del canale, non la percentuale.
Vale qualcosa di simile per il **capitale privato**, ma solo dove il privato cofinanzia il proprio
investimento: negli incentivi alle imprese chi mette dei soldi propri è a rischio nel 31,8% dei
casi contro il 36,6%, mentre altrove la differenza sparisce.

E i due sospettati di partenza? La **dimensione** pesa, ma il rischio non cresce all'infinito:
è massimo nelle fasce intermedie. Il **numero di enti coinvolti** invece esce assolto in via
definitiva: a parità del resto, più mani sul progetto non significano più rischio (odds ratio
0,96, semmai leggermente meno).

<!-- GRAFICO · versione divulgativa del forest plot, generata da
     01_analisi/figure/make_mod_landing_or.py (numeri TRASCRITTI dal nb 02 §3, non ricalcolati:
     se il modello viene rieseguito va aggiornata la lista OR nello script). Stessa grammatica
     del forest plot della pagina Regressione (pallino + baffi dell'IC, scala logaritmica, stessa
     palette): cambiano solo il numero di righe e le etichette, in italiano corrente invece che
     nei nomi delle dummy. AREA_NON_TERR escluso, come là. -->

<figure class="fig-home">
  <img src="{{ site.baseurl }}/assets/images/modello/mod_landing_or.png"
       alt="Grafico a pallini con intervalli di confidenza: il Mezzogiorno è il fattore più forte a 2,80, seguito da contributi ad altri soggetti a 2,34 e competitività delle imprese a 2,14; il numero di enti resta a 0,96, cioè praticamente neutro">
  <figcaption>
    Gli otto fattori di cui parla questo capitolo, messi a confronto <strong>a parità di tutto il
    resto</strong>. Ogni pallino dice quante volte cambiano le probabilità di finire a rischio
    rispetto a un progetto di riferimento, e la linea sottile attorno è il margine di incertezza.
    In cima c'è il territorio, non la dimensione né la governance: il <strong>numero di enti
    coinvolti</strong>, il sospettato di partenza, è quel pallino praticamente fermo sull'1. È la
    stessa figura che trovate <a href="{{ site.baseurl }}/regressione.html#odds-ratio">nella pagina
    della regressione</a>, lì con tutti i fattori e le verifiche.
  </figcaption>
</figure>

<!-- ✅ RANDOM FOREST · dal notebook 04, numeri riverificati rieseguendo il modello:
     AUC 0,813 sul test contro 0,669 della logistica sullo stesso split; SHAP mette il
     territorio in cima; la quota UE ha 74.302 valori distinti e arrotondandola l'AUC
     scende a 0,778 (10%) e 0,732 (sì/no). PROSA DA RIFINIRE COL GRUPPO. -->
A questo punto la domanda diventa un'altra: se sappiamo *che cosa* rende fragile un progetto,
riusciamo a **riconoscerlo in anticipo**? Abbiamo messo alla prova un secondo modello, un
[Random Forest]({{ site.baseurl }}/random-forest.html), che invece di misurare il peso di ogni
fattore cerca da solo le combinazioni che portano al blocco. Prevede nettamente meglio della
regressione, abbastanza da costruire una **lista di sorveglianza**: non per dire «questo progetto
fallirà», ma per dire quali meritano un controllo prima degli altri. E interrogato su quali
informazioni usi, mette **il territorio al primo posto**, pur non sapendo nulla del verdetto della
regressione ed essendo libero di dare peso a qualunque cosa. E non si ferma lì: interrogato sui
tipi di intervento e sui temi, li mette **nello stesso ordine** della regressione, dai contributi
ad altri soggetti in cima all'acquisto di beni in fondo. Due modelli costruiti su logiche opposte
arrivano allo stesso indiziato e alla stessa classifica.

C'è però un dettaglio che dice molto sul funzionamento reale della macchina pubblica. Una parte
consistente della capacità di previsione non viene dalle caratteristiche del progetto, ma dai
**decimali del suo piano di finanziamento**: cifre che identificano il bando da cui il progetto è
nato. Semplificando quel dato, la capacità predittiva cala sensibilmente. Tradotto: per indovinare
quali progetti si fermeranno, sapere **da quale programma arrivano** conta quasi quanto sapere
**come sono fatti**.

<!-- GRAFICO · confronto AUC (dalla pagina Random Forest, già in palette del sito).
     Regge da solo i due capoversi qui sopra: il salto rispetto alla regressione E il fatto che
     metà del salto sparisce quando si sfoca il piano di finanziamento. -->

<figure class="fig-home">
  <img src="{{ site.baseurl }}/assets/images/modello/rf_confronto_auc.png"
       alt="Barre orizzontali: la capacità di previsione passa da 0,669 della regressione a 0,813 del Random Forest, ma scende a 0,732 se si semplificano le quote di finanziamento">
  <figcaption>
    Quanto bene i modelli riconoscono in anticipo un progetto a rischio, misurato su progetti
    <strong>mai visti prima</strong> (0,5 = tirare a indovinare, 1 = previsione perfetta). Il
    Random Forest stacca nettamente la regressione. Ma le due barre centrali mostrano il prezzo
    della trasparenza: sfocando i decimali del piano di finanziamento, cioè togliendo al modello
    la possibilità di riconoscere il bando, il vantaggio si dimezza. Il dettaglio del calcolo è
    <a href="{{ site.baseurl }}/random-forest.html">nella pagina dedicata</a>.
  </figcaption>
</figure>

# Cosa fare: il bicchiere, il verdetto e una via d'uscita {#cosa-fare}

<!-- ATTO III · climax, risoluzione, speranza, call to action.
     Assorbe la vecchia pagina conclusions.html (dismessa il 14/07/2026). BOZZA. -->

<figure style="margin: 1.5rem 0;">
  <img src="{{ site.baseurl }}/assets/images/hero_conclusions.jpg" alt="Svincolo autostradale visto dall'alto"
       style="width: 100%; border-radius: 4px;">
  <figcaption style="font-size: 0.8rem; color: #888; margin-top: 0.4rem;">
    I fondi arrivano a destinazione solo se il percorso non si interrompe.
  </figcaption>
</figure>

Il climax della storia è amaro: misurata sul suo obiettivo dichiarato (l'equità territoriale),
la politica di coesione **manca il bersaglio proprio dove punta**: gli esiti sono
sistematicamente peggiori nel Mezzogiorno, che dei fondi è il primo destinatario.

Ma il bicchiere non è vuoto, e dirlo è parte dell'onestà del racconto. I cicli che hanno avuto
il tempo di finire la corsa **arrivano in fondo**: il 2000-2006 è concluso al 76,5%, il
2007-2013 al 66%: il sistema, col tempo, chiude. Metà dei progetti spende praticamente tutto
il proprio budget (assorbimento mediano 0,986). Ci sono regioni che funzionano (la Liguria
conclude il 76,4% con appena il 9,2% a rischio) e temi che viaggiano bene, come **energia** e
**reti digitali** (conclusi al 64% e 69%, rischio sotto il 25%). Il problema non è "nulla
funziona": è che il funzionamento è **diseguale**, e la disuguaglianza ricalca proprio i divari
che i fondi dovrebbero chiudere.

<!-- GRAFICO · classifica regionale dei conclusi: sostiene "ci sono regioni che funzionano"
     e mostra apertamente l'eccezione Lazio (meglio dichiararla noi che farla scoprire). -->

<figure class="fig-home fig-home--narrow">
  <img src="{{ site.baseurl }}/assets/images/eda/08_regioni.png"
       alt="Classifica delle regioni per percentuale di progetti conclusi: Liguria prima, Sicilia ultima">
  <figcaption>
    Il bicchiere, regione per regione: in testa la Liguria (76,4% concluso), in coda la Sicilia
    (31,1%). Il gradiente Nord–Sud ha però un'eccezione vistosa: il <strong>Lazio</strong>,
    penultimo pur essendo Centro-Nord: segno che la geografia non spiega tutto da sola.
  </figcaption>
</figure>

## Cosa ci portiamo a casa

Tre messaggi che reggono da soli, prima ancora del verdetto del modello. Primo: **contare i
progetti inganna**, vanno pesati per importo. I progetti sotto il mezzo milione sono il **70% del
totale** ma valgono 31 miliardi sui 315: chi conta le pratiche vede un Paese di piccoli interventi,
chi conta i soldi ne vede un altro. E l'anello debole non sta dove ce lo si aspetta:
il rischio è massimo sui progetti medio-grandi (43,9% fra 5 e 10 milioni), mentre i 623 giganti
sopra i 50 milioni, pur rischiando meno in proporzione, valgono da soli 120 miliardi. Secondo:
c'è un **falso colpevole**, la complessità di governance, misurata dal numero di enti coinvolti,
non spiega il rischio; le apparenti eccezioni riportano a pochi programmi in due regioni del Sud.
Terzo: il **divario Nord-Sud non è un incidente di percorso**, persiste in ogni ciclo nonostante
al Sud arrivino più fondi. La leva più concreta che emerge dai dati descrittivi non è *quanti*
soldi arrivano, ma *come sono disegnati* i progetti e *chi ha gli strumenti* per spenderli.

<!-- ✅ FRASE FINALE · riempita il 16/07/2026 col verdetto del modello (nb 02: territorio
     rilevante a parità di composizione). PROPOSTA: prosa da validare col gruppo. -->
E il verdetto sugli indiziati è arrivato: la dimensione conta, il tipo di intervento conta molto,
ma **il territorio pesa anche a parità di tutto il resto**: stesso importo, stesso tema, stesso
tipo di opera, stessi fondi, un progetto del Mezzogiorno parte comunque con odds di rischio quasi
tre volte più alte. Il divario non è il riflesso di come sono fatti i progetti: è il segno che,
per arrivare in fondo, conta ancora **dove** un progetto nasce.

## E adesso? Due leve (e una parte che spetta a te)

<!-- BOZZA CTA · tono: speranza operosa, niente retorica. Da rifinire con il gruppo. -->

Se l'ipotesi dell'antagonista è giusta, la risposta non è (solo) più soldi: è **più capacità di
spenderli**. La prima leva è la **formazione e il rafforzamento dei funzionari pubblici**,
soprattutto nei piccoli comuni del Mezzogiorno: concorsi, competenze tecniche, assistenza alla
progettazione. La seconda è la **pressione sulle politiche locali**: i dati di OpenCoesione sono
pubblici proprio perché i cittadini possano chiedere conto dei progetti dei propri territori.
Ogni progetto fermo ha un nome, un importo e un responsabile consultabili da chiunque. Qui entri
in gioco tu: cerca il tuo comune su [OpenCoesione](https://opencoesione.gov.it), guarda che fine
hanno fatto i suoi progetti, e chiedi. **I soldi per l'equità ci sono già: quello che manca si
può costruire.**

<!-- 🎙️ INTERVISTA (citazione estesa): riempito il 16/07/2026 con citazioni VERBATIM dalla
     trascrizione (selezione completa in Data Journalism e struttura/virgolettati_intervista.md).
     ⚠️ DA AUTORIZZARE prima della pubblicazione (l'intervistato rivedrà il lavoro). L'esperienza
     dell'intervistato è PNRR/fondi nazionali: le sue parole descrivono la macchina amministrativa
     pubblica, NON sono testimonianza specifica sui fondi di coesione: contesto dichiarato nel testo.
     Stessa voce che apre l'articolo (frase breve dopo il contesto 5W). -->
<div style="border-left: 4px solid #D1573B; padding: 0.6rem 0 0.6rem 1.2rem; margin: 2rem 0;">
  <p style="font-size: 0.95rem; color: #2b2b2b; margin-bottom: 0.5rem;">
    🎙️ <strong>La voce di chi i fondi li gestisce.</strong> Il dirigente del CNR che apre questo
    articolo gestisce fondi PNRR e nazionali, un canale diverso dalla coesione, ma la stessa
    macchina pubblica che deve trasformare i finanziamenti in risultati. Dal campo, l'antagonista
    che abbiamo solo ipotizzato ha un volto concreto:
  </p>
  <p style="font-size: 1.05rem; color: #2b2b2b; margin-bottom: 0.5rem;">
    «Qualsiasi attività di ricerca non è soltanto ideazione e articolo pubblicato: c'è tutta una
    serie di procedure contabili che devono essere gestite dal personale amministrativo, e di
    questo noi abbiamo una grande carenza, come CNR ma in generale come Paese. Siamo molto più
    in basso rispetto alla Spagna o alla Francia.»
  </p>
  <p style="font-size: 0.95rem; color: #2b2b2b; margin-bottom: 0.5rem;">
    E alla domanda sul divario territoriale, la sua risposta tiene insieme il bicchiere e il verdetto:
  </p>
  <p style="font-size: 1.05rem; color: #2b2b2b; margin-bottom: 0.5rem;">
    «Io personalmente vedo il bicchiere sempre pieno […]: ci sono moltissime eccellenze, ma il
    sistema non è solido come Paese, e quindi necessariamente ci sono gruppi più forti che vanno
    più avanti, e tendenzialmente sono nella parte del Centro-Nord su molte partite.»
  </p>
  <p style="font-size: 0.95rem; color: #2b2b2b; margin-bottom: 0.5rem;">
    Anche la via d'uscita, vista dal campo, è la stessa che indicano i dati, cioè investire sulle
    persone che fanno camminare i fondi: «La Spagna, per esempio, con i fondi del PNRR ha
    formato moltissime persone nel capire e scrivere il progetto europeo […] in Spagna c'è stato
    un piano di formazione, un intervento da parte dello Stato, come non c'è stato da noi.»
  </p>
  <p style="font-size: 0.95rem; color: #2b2b2b; margin-bottom: 0.5rem;">
    Ma non serve guardare all'estero per trovare la prova che la leva funziona. Ce n'è una italiana,
    ed è la ragione per cui questa storia non finisce in pessimismo:
  </p>
  <p style="font-size: 1.05rem; color: #2b2b2b; margin-bottom: 0.5rem;">
    «L'Università di Bologna, qualche anno fa, ha cambiato il direttore generale; è arrivato un
    direttore proveniente dall'impresa, che ha chiamato a raccolta cinquanta persone capaci e ha
    creato un grosso gruppo che doveva dare supporto ai ricercatori e al personale […] per
    partecipare ai progetti europei. Sono stati talmente bravi ed efficaci che l'allora ministro
    […] ha chiamato questo professore al ministero come consulente, per capire come diffondere
    questo approccio anche ad altri.»
  </p>
  <p style="font-size: 0.95rem; color: #2b2b2b; margin-bottom: 0.5rem;">
    Cinquanta persone assunte per aiutare gli altri a spendere: è esattamente la variabile che
    manca ai territori dove i progetti si fermano, e non è una riforma costituzionale. È una
    decisione organizzativa.
  </p>
  <p style="font-size: 0.82rem; color: #888; margin: 0;">
    Dalla trascrizione dell'intervista, luglio 2026 · citazioni in attesa di revisione finale dell'intervistato
  </p>
</div>

## I limiti di questa storia

Quattro avvertenze prima di leggere tutto questo come una verità definitiva. Primo: le
differenze descrittive non bastano da sole, ed è per questo che il passo decisivo è il modello.
Secondo: il **ritardo** è misurato quasi solo sui progetti con una fine effettiva, quindi le
analisi sui tempi vanno prese con prudenza. Terzo: nella nostra definizione di "concluso" i
progetti **liquidati** (un ulteriore 6,9%) sono esclusi: includendoli si sale al 55,8%. La
sostanza del racconto non cambia, ma il numero sì. Quarto: qui guardiamo la sola politica di
**coesione**, e il **PNRR resta fuori**: è un canale con regole, tempistiche e sistemi di
monitoraggio diversi, e questa analisi non dice nulla su di esso. Infine, una domanda che il dataset non
può chiudere: *che fine fanno i soldi dei progetti che non si concludono?* Possiamo dire quanti
sono fermi (122,5 miliardi nei progetti a rischio, 45,5 già pagati), ma non il loro destino:
riprogrammazioni e disimpegni non sono tracciati qui.

<!-- 🎙️ INTERVISTA (quarta occorrenza): citazioni VERBATIM, sezione E di virgolettati_intervista.md.
     Non è un risultato nostro: è il meccanismo raccontato dall'intervistato sui fondi che gestisce
     lui (PNRR/nazionali), usato per dire che cosa il nostro dataset NON vede. Contesto dichiarato.
     ⚠️ DA AUTORIZZARE come le altre, e in particolare da far rivedere: il dettaglio dell'euro di
     morosità riguarda il suo ente e potrebbe volerlo togliere. -->
Il meccanismo, però, ce lo ha raccontato la stessa voce che attraversa questo articolo, riferendosi
ai fondi che gestisce lui: «se il finanziatore ha dato dei soldi e tu non li hai spesi, glieli
restituisci; se li hai spesi ma non hai raggiunto gli obiettivi, glieli devi comunque restituire».
E la parte che i nostri numeri non mostrano viene dopo: l'ente che non restituisce risulta moroso,
e la morosità blocca gli incassi di **tutti** i suoi altri progetti, compresi quelli che stavano
andando bene. Al momento dell'intervista il suo ente aveva un euro di morosità su un progetto, e
per quell'euro altri progetti non potevano ricevere i saldi. «Può avere conseguenze che vanno oltre
il progetto […] diventa un "effetto domino", una reazione a catena.» Se vale anche per la coesione,
il costo di un progetto fermo non si esaurisce in quel progetto: è forse la domanda più interessante
che lasciamo aperta, e i nostri dati non possono chiuderla.

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
