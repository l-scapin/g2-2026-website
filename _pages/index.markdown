---
# Landing = ARTICOLO (una sola pagina lunga, scrollytelling con ancore — deciso il 14/07/2026).
# La navbar punta alle ancore: #il-problema · #perche-succede · #cosa-fare
# Per modificare il layout: https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: "Home"
vega: true
header_type: splash #base, post, hero, image, splash — splash = pagina intera, titolo centrato
header_img: assets/images/hero_road.jpg
header_title: "Where Does the Money Go?"
subtitle: "315 miliardi per riequilibrare l'Italia. Ma i progetti si fermano proprio dove servono di più: al Sud il rischio è doppio che al Nord."

---

<!-- ═══════════════════════════════════════════════════════════════════
     BOZZA v1 — 14/07/2026. Articolo in 3 atti. Convenzioni degli slot:
     ⚠️ [DA COMPLETARE …]  = numeri/esiti che arrivano da analisi non ancora definitive
     🎙️ SLOT INTERVISTA    = MAI virgolettati inventati; testo neutro finché non ci sono
                             parole reali autorizzate. L'intervistato ("Magnifico") si occupa
                             di PNRR: le sue parole vanno CONTESTUALIZZATE (esperienza di
                             gestione di fondi pubblici), non spacciate per testimonianza
                             sui fondi di coesione, che sono un canale diverso.
     [DATO ISTAT DA INSERIRE] = data-hero sul contesto: cercare e verificare prima di scrivere.
     TODO scrollytelling: il tema ha scrollama (vedi demo) — da valutare sugli atti in seconda battuta.
     Tutti i numeri già presenti sono VERIFICATI (RECAP.md, 12-14/07/2026). Non arrotondare 31,5 → 31.
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
il divario **resiste dentro ogni ciclo** di programmazione. Questa è la storia di dove i soldi
si fermano — e di che cosa si inceppa.
{: .lead }

# Che cos'è la politica di coesione (e perché ti riguarda) {#coesione}

**Che cosa.** La politica di coesione è lo strumento con cui l'Unione Europea e lo Stato
finanziano interventi per ridurre i divari tra territori: infrastrutture, ricerca, ambiente,
scuole, servizi. **Chi paga**: fondi europei (FESR, FSE) più un consistente cofinanziamento
nazionale — il solo Fondo Sviluppo e Coesione vale circa 99 miliardi. In entrambi i casi la
fonte ultima è la stessa: le tasse di tutti. **Quanto**: nei progetti monitorati da
**OpenCoesione** — il portale pubblico che li documenta uno per uno — passano oltre **315
miliardi di euro** di finanziamento pubblico. **Dove e quando**: in tutta Italia, per cicli di
programmazione di sette anni (dal 2000-2006 al 2021-2027), con più risorse al Mezzogiorno,
coerentemente con la missione redistributiva. **Perché**: l'obiettivo dichiarato è l'**equità
territoriale** — che nascere a Enna o a Bolzano non determini la qualità dei servizi a cui hai
accesso. Noi analizziamo i progetti da almeno 100.000 € (il PNRR è un canale diverso e resta
fuori) con i metodi statistici presentati nelle [pagine tecniche](#approfondire).

<!-- CONTESTO INEGUAGLIANZA — data hero ISTAT, da verificare PRIMA di pubblicare. -->
> **[DATO ISTAT DA INSERIRE — contesto]** Qui una o due frasi con dati ISTAT verificati
> sull'ineguaglianza territoriale: popolazione del Mezzogiorno, migrazione interna Sud→Nord
> (in particolare dei giovani laureati), eventualmente un indicatore di servizi (asili nido,
> tempo pieno, trasporti). Nessun numero va scritto qui prima di averlo verificato alla fonte.

<!-- 🎙️ SLOT INTERVISTA (frase breve) — regola: MAI virgolettati non realmente pronunciati.
     Quando l'intervista sarà fatta e autorizzata: qui UNA frase breve e d'effetto (max 2 righe);
     la citazione estesa va nell'Atto III — stessa voce che apre e chiude il racconto.
     ⚠️ Contestualizzare: l'intervistato lavora sul PNRR, non sulla coesione. -->
<div style="border-left: 4px solid #177E89; padding: 0.6rem 0 0.6rem 1.2rem; margin: 2.2rem 0;">
  <p style="font-size: 1.05rem; color: #2b2b2b; margin-bottom: 0.5rem;">
    🎙️ <strong>La voce di chi i fondi li gestisce.</strong> Stiamo intervistando un dirigente con
    esperienza diretta nella gestione di fondi pubblici: la sua lettura di questi numeri comparirà qui.
  </p>
  <p style="font-size: 0.82rem; color: #888; margin: 0;">
    Intervista in corso — 2026
  </p>
</div>

# Il problema: i progetti si fermano dove servono di più {#il-problema}

<!-- ATTO I — inciting event. BOZZA: prosa da rifinire, numeri già verificati. -->

Il protagonista di questa storia non è una persona: sono i **fondi di coesione**, 315 miliardi
di euro con una missione scritta nei trattati — riequilibrare i territori. Il loro oggetto del
desiderio è l'**equità territoriale**. E come in ogni storia, a un certo punto qualcosa si
inceppa: **non tutti i progetti si concludono, e falliscono più spesso proprio dove servirebbero
di più**.

I numeri dell'inciampo, alla data di riferimento (6 maggio 2025): dei 206.777 progetti,
è concluso il **48,9%**, mentre il **31,5%** è **a rischio**. Al Centro-Nord il rischio tocca il
**20,1%** dei progetti; nel Mezzogiorno il **40,3%**: **il doppio**. Eppure il Sud gestisce
**215 miliardi** contro i 79 del Centro-Nord: i soldi ci sono, è il percorso che si interrompe.

<!-- BOX DEFINIZIONE — "a rischio" è la nostra variabile chiave e la definiamo noi:
     va dichiarata in modo inequivocabile. Numeri verificati sul dataset (15/07/2026). -->
<div class="def-box">
  <p class="def-box__label">La nostra variabile chiave</p>
  <h4>Quando un progetto è «a rischio»?</h4>
  <p>Non esiste un'etichetta ufficiale: <strong>l'abbiamo costruita noi</strong>, da due segnali
  osservabili nei dati alla data di riferimento (6 maggio 2025). Un progetto è «a rischio» se:</p>
  <p><strong>1 · non è mai partito</strong> — risulta ancora «non avviato»
  (16.261 progetti, il 7,9%), <em>oppure</em><br>
  <strong>2 · è fuori tempo massimo</strong> — è «in corso» ma la sua data di fine prevista
  è già passata (48.910 progetti, il 23,7%).</p>
  <p>In totale: <strong>65.171 progetti, il 31,5%</strong>. «A rischio» non significa fallito:
  significa che il percorso si è inceppato e l'esito è in dubbio.</p>
  <p class="def-box__note">Nota di trasparenza: un progetto <em>concluso</em> in ritardo non conta
  come a rischio — la definizione guarda chi è ancora per strada, non chi è arrivato tardi. Ed è la
  fotografia di un istante: un progetto oggi a rischio può ancora arrivare in fondo.</p>
</div>

<!-- GRAFICO · Sankey (versione leggera, esatta all'euro — la stessa dell'EDA).
     Risponde letteralmente al titolo del sito: da dove arrivano i soldi e dove vanno.
     La legenda completa dei fondi resta nell'EDA: qui solo la lettura essenziale. -->

<figure class="fig-home">
  <iframe src="{{ site.baseurl }}/assets/charts/plotly/sankey_fondi.html"
          title="Diagramma di Sankey: il percorso dei fondi dalla fonte al territorio al tema"
          style="width: 100%; height: 520px; border: none;"
          loading="lazy"></iframe>
  <figcaption>
    Il percorso dei 315 miliardi, esatto all'euro: da ogni <strong>fonte</strong> — europea (FESR, FSE)
    o nazionale (FSC, PAC, rotazione) — al <strong>territorio</strong>, fino al <strong>tema</strong>. Lo spessore dei
    flussi è proporzionale ai fondi pubblici. Due letture: al Sud la coesione è più nazionale (FSC)
    che europea, e i trasporti assorbono la fetta maggiore. Passa il mouse sui flussi per i valori;
    la legenda completa delle fonti è <a href="{{ site.baseurl }}/eda.html#dove-passano-i-fondi">nell'EDA</a>.
  </figcaption>
</figure>

E parliamo di cifre che si fanno fatica a immaginare: nei progetti a rischio sono impegnati
**115,6 miliardi di euro** di finanziamento pubblico — più di un terzo dell'intero portafoglio —
di cui risultano pagati finora solo 43,2. Ci sono **26,3 miliardi** fermi in 16.261 progetti
**mai avviati**, con zero pagamenti. E la geografia del denaro fermo ricalca quella del bisogno:
**93,5 miliardi a rischio nel Mezzogiorno**, 17,5 nel Centro-Nord.

<!-- GRAFICO · Mappa del rischio (statica, dall'EDA — era il candidato indicato per l'Atto I).
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
un progetto si ferma al Sud, l'equità territoriale — la ragione per cui quei fondi esistono —
si allontana esattamente dove era più urgente.

# Perché succede: l'identikit del rischio (e un falso colpevole) {#perche-succede}

<!-- ATTO II — effetti + antagonista. BOZZA: prosa da rifinire, numeri verificati il 12-14/07. -->

Se il problema fosse casuale, colpirebbe a caso. Invece ha un identikit preciso. Il rischio
cresce con la **dimensione**: i progetti piccoli si concludono nel 53,6% dei casi, quelli sopra
i 50 milioni solo nel **13,8%** — e i 623 progetti giganti valgono da soli 120,5 miliardi. Cresce
con la **giovinezza del ciclo**: il 2014-2020 è a rischio al 36,0%, il 2021-2027 già al 36,5%
quando la corsa è appena iniziata. Cambia con il **tema**: in testa la **competitività delle
imprese** (37,7% a rischio, ed è anche il tema con meno progetti conclusi), poi **trasporti**
(35,5%) e **ambiente** (33,6%) — mentre welfare e istruzione, contrariamente a quanto si
potrebbe pensare, stanno alla media o sotto. E soprattutto cresce **a Sud**, dentro ogni ciclo
di programmazione: il divario Centro-Nord/Mezzogiorno nei conclusi è **persistente**, non
l'effetto di una stagione sfortunata.

<!-- GRAFICI · i due tratti più netti dell'identikit: dimensione e persistenza del divario.
     Il tema resta solo nel testo (il grafico per tema è nell'EDA): tre figure di fila
     appesantirebbero l'atto. -->

<figure class="fig-home">
  <img src="{{ site.baseurl }}/assets/images/eda/05_dimensione.png"
       alt="Grafico a barre: la percentuale di progetti conclusi cala al crescere della classe di importo, dal 53,6% al 13,8%">
  <figcaption>
    Più grandi, più fragili: la conclusione scende dal 53,6% dei progetti piccoli (100–500k €)
    al 13,8% degli oltre 50 milioni. E la spesa segue lo stesso gradiente: l'assorbimento
    cala da 0,75 a 0,42.
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
— più enti, più tavoli, più firme — siano i più fragili. I dati dicono di no: la correlazione
tra numero di enti e rischio è praticamente nulla, e i progetti con più di 5 enti sono anzi i
*meno* a rischio. L'apparente eccezione (un picco di rischio nei progetti con 3 enti) svanisce
guardando da vicino: è quasi tutta concentrata in pochi programmi del ciclo 2007-2013, in
Sicilia e Calabria. Anche il falso colpevole, insomma, riporta al territorio.

E qui entra in scena l'**antagonista** — che non abita nel dataset. I dati OpenCoesione dicono
*dove* e *quanto* i progetti si fermano, non *chi* o *che cosa* li ferma. L'ipotesi più
accreditata in letteratura è la **capacità amministrativa**: organici ridotti, competenze
progettuali scarse, uffici tecnici che devono gestire pratiche complesse senza le persone per
farlo. Se è così, il paradosso è crudele: **chi più avrebbe bisogno dei fondi, meno ha gli
strumenti per spenderli**. I fondi possono comprare cemento e servizi, ma non possono comprare
da soli la macchina amministrativa che serve a spenderli.

<!-- 📚 SLOT FONTI ANTAGONISTA — l'ipotesi "capacità amministrativa" è FUORI dal nostro dataset:
     va sostenuta SOLO con citazioni reali da fonti pubblicate, con riferimento esatto
     (relazioni Corte dei Conti sui fondi SIE; rapporti SVIMEZ; studi Banca d'Italia).
     Trovare il passaggio, citarlo tra virgolette CON fonte e anno, o non citare affatto. -->
> **[CITAZIONE DA FONTE PUBBLICATA — DA INSERIRE]** Qui un passaggio reale e referenziato
> (Corte dei Conti / SVIMEZ / Banca d'Italia) a sostegno dell'ipotesi sulla capacità
> amministrativa. Finché non c'è, l'ipotesi resta dichiarata come tale nel paragrafo sopra.

<!-- ⚠️ SLOT MODELLO — da completare con i risultati DEFINITIVI del Notebook 02.
     Scritto per reggere QUALSIASI esito: scegliere l'esito vero, non piegare i dati alla frase.
     Il preliminare esiste (logistica IRLS) ma i numeri NON vanno pubblicati finché non sono finali. -->
> **[DA COMPLETARE — risultato del modello]** Ma il territorio conta *di per sé*, o è solo il
> riflesso di dimensione, ciclo e tema dei progetti che ospita? Il **modello multivariato**
> (pagina [modello]({{ site.baseurl }}/modello.html)) mette tutti i fattori sullo stesso piano.
> **[Esito A: il territorio resta tra i fattori più rilevanti → il divario non si spiega con la
> composizione dei portafogli. / Esito B: pesano soprattutto dimensione e ciclo → più che un
> "problema Sud", un problema di come sono fatti i progetti.]** In entrambi i casi è una notizia.
> Nello stesso modello verifichiamo formalmente anche il ruolo del numero di enti coinvolti:
> **[risultato]**.

# Cosa fare: il bicchiere, il verdetto e una via d'uscita {#cosa-fare}

<!-- ATTO III — climax, risoluzione, speranza, call to action.
     Assorbe la vecchia pagina conclusions.html (dismessa il 14/07/2026). BOZZA. -->

<figure style="margin: 1.5rem 0;">
  <img src="{{ site.baseurl }}/assets/images/hero_conclusions.jpg" alt="Svincolo autostradale visto dall'alto"
       style="width: 100%; border-radius: 4px;">
  <figcaption style="font-size: 0.8rem; color: #888; margin-top: 0.4rem;">
    I fondi arrivano a destinazione solo se il percorso non si interrompe.
  </figcaption>
</figure>

Il climax della storia è amaro: misurata sul suo obiettivo dichiarato — l'equità territoriale —
la politica di coesione **manca il bersaglio proprio dove punta**: gli esiti sono
sistematicamente peggiori nel Mezzogiorno, che dei fondi è il primo destinatario.

Ma il bicchiere non è vuoto, e dirlo è parte dell'onestà del racconto. I cicli che hanno avuto
il tempo di finire la corsa **arrivano in fondo**: il 2000-2006 è concluso al 76,5%, il
2007-2013 al 66% — il sistema, col tempo, chiude. Metà dei progetti spende praticamente tutto
il proprio budget (assorbimento mediano 0,986). Ci sono regioni che funzionano — la Liguria
conclude il 76,4% con appena il 9,1% a rischio — e temi che viaggiano bene, come **energia** e
**reti digitali** (conclusi al 64% e 69%, rischio sotto il 21,4%). Il problema non è "nulla
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
    penultimo pur essendo Centro-Nord — segno che la geografia non spiega tutto da sola.
  </figcaption>
</figure>

## Cosa ci portiamo a casa

Tre messaggi restano in piedi qualunque cosa dica il modello. Primo: **contare i progetti
inganna** — vanno pesati per importo, e i progetti grandi sono l'anello debole del sistema
(sopra i 50 milioni si conclude il 13,8%). Secondo: c'è un **falso colpevole** — la complessità
di governance, misurata dal numero di enti coinvolti, non spiega il rischio; le apparenti
eccezioni riportano a pochi programmi in due regioni del Sud. Terzo: il **divario Nord-Sud non
è un incidente di percorso** — persiste in ogni ciclo, nonostante al Sud arrivino più fondi. La
leva più concreta che emerge dai dati descrittivi non è *quanti* soldi arrivano, ma *come sono
disegnati* i progetti — e *chi ha gli strumenti* per spenderli.

<!-- ⚠️ FRASE FINALE — da chiudere col verdetto del modello: territorio o dimensione? -->
**[DA COMPLETARE — la chiusura del racconto: quale dei due indiziati pesa di più?]**

## E adesso? Due leve (e una parte che spetta a te)

<!-- BOZZA CTA — tono: speranza operosa, niente retorica. Da rifinire con il gruppo. -->

Se l'ipotesi dell'antagonista è giusta, la risposta non è (solo) più soldi: è **più capacità di
spenderli**. La prima leva è la **formazione e il rafforzamento dei funzionari pubblici**,
soprattutto nei piccoli comuni del Mezzogiorno: concorsi, competenze tecniche, assistenza alla
progettazione. La seconda è la **pressione sulle politiche locali**: i dati di OpenCoesione sono
pubblici proprio perché i cittadini possano chiedere conto dei progetti dei propri territori —
ogni progetto fermo ha un nome, un importo e un responsabile consultabili da chiunque. Qui entri
in gioco tu: cerca il tuo comune su [OpenCoesione](https://opencoesione.gov.it), guarda che fine
hanno fatto i suoi progetti, e chiedi. **I soldi per l'equità ci sono già: quello che manca si
può costruire.**

<!-- 🎙️ SLOT INTERVISTA (citazione estesa) — regola: MAI virgolettati non realmente pronunciati.
     Qui la CITAZIONE ESTESA autorizzata; in apertura la stessa voce con una frase breve.
     ⚠️ L'intervistato si occupa di PNRR: introdurlo per quello che è (esperienza diretta di
     gestione/attuazione di fondi pubblici, canale PNRR) e usare le sue parole sul funzionamento
     della macchina amministrativa — NON come testimonianza specifica sui fondi di coesione. -->
<div style="border-left: 4px solid #D1573B; padding: 0.6rem 0 0.6rem 1.2rem; margin: 2rem 0;">
  <p style="font-size: 1.05rem; color: #2b2b2b; margin-bottom: 0.5rem;">
    🎙️ <strong>La voce di chi i fondi li gestisce.</strong> Qui entrerà l'intervista a un dirigente
    con esperienza diretta nella gestione di fondi pubblici: che cosa vede, dal campo, dietro questi numeri?
  </p>
  <p style="font-size: 0.82rem; color: #888; margin: 0;">
    Intervista in corso — 2026
  </p>
</div>

## I limiti di questa storia

Quattro avvertenze prima di leggere tutto questo come una verità definitiva. Primo: le
differenze descrittive non bastano da sole, ed è per questo che il passo decisivo è il modello.
Secondo: il **ritardo** è misurato quasi solo sui progetti con una fine effettiva, quindi le
analisi sui tempi vanno prese con prudenza. Terzo: nella nostra definizione di "concluso" i
progetti **liquidati** (un ulteriore 6,9%) sono esclusi: includendoli si sale al 55,8% — la
sostanza del racconto non cambia, ma il numero sì. Quarto: qui guardiamo la sola politica di
**coesione** — il **PNRR resta fuori**, e confrontare i due canali richiede cautela metodologica
(regole, tempistiche e sistemi di monitoraggio diversi). Infine, una domanda che il dataset non
può chiudere: *che fine fanno i soldi dei progetti che non si concludono?* Possiamo dire quanti
sono fermi (115,6 miliardi nei progetti a rischio, 43,2 già pagati), ma non il loro destino —
riprogrammazioni e disimpegni non sono tracciati qui.

# Per approfondire: il percorso tecnico {#approfondire}

Questa storia poggia su un percorso analitico completo, documentato nelle pagine tecniche.

<div class="qcards">
  <div class="qcard">
    <h5>Si concludono?</h5>
    <p>Quanti arrivano davvero a chiusura — e perché i progetti grandi si fermano più spesso.</p>
    <a href="{{ site.baseurl }}/eda.html">Esplorazione dei dati (EDA) →</a>
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

<p style="text-align: center; font-size: 0.85rem; color: #888; margin-top: 1.2rem;">
  In arrivo: <a href="{{ site.baseurl }}/modello.html">modello predittivo del rischio</a> ·
  <a href="{{ site.baseurl }}/clustering.html">clustering dei profili regionali</a> ·
  <a href="{{ site.baseurl }}/text-analysis.html">text analysis delle descrizioni</a>
</p>

<hr>

<p style="font-size: 0.8rem; color: #888; margin-top: 1.5rem;">
  Immagine di copertina: foto di <a href="https://unsplash.com/photos/zN4mtLHkHn4" target="_blank" rel="noopener">Fahrul Azmi</a> su <a href="https://unsplash.com" target="_blank" rel="noopener">Unsplash</a>.
  Svincolo aereo: foto di <a href="https://unsplash.com/photos/zBrnXi2IgpY" target="_blank" rel="noopener">Rodrigo Kugnharski</a> — Parco del Portello, Milano, su <a href="https://unsplash.com" target="_blank" rel="noopener">Unsplash</a>.
</p>
