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

Prima di modellare qualsiasi cosa, guardiamo i dati. Lavoriamo su **206.777 progetti**
della politica di coesione italiana (fonte: dati aperti **OpenCoesione**, solo progetti da
almeno 100.000 € e pubblicati). L'esplorazione ruota su una domanda sola: quali progetti sono
**a rischio**, e dove si concentrano?
{: .lead }

# Qualità e preparazione dei dati

Il dataset non ha righe duplicate: ogni progetto è identificato in modo univoco dalla coppia
CUP + codice locale. I valori mancanti ci sono, ma quasi tutti sono *strutturali*, non errori.
Per esempio, il ritardo e la data di fine effettiva mancano sui progetti non ancora conclusi,
semplicemente perché una fine non c'è ancora. Le descrizioni tematiche e il fondo europeo mancano
invece sui progetti a finanziamento puramente nazionale (FSC, PAC): anche questo è atteso, non un buco.

Prima di ogni analisi fine teniamo a mente due trappole nei dati: alcuni pagamenti sono
**negativi** (rettifiche contabili, pochi ma da azzerare nelle somme), e circa l'1% dei progetti è
**multi-regione**, con i nomi delle regioni concatenati da `:::`, e vanno esclusi prima di
costruire mappe o classifiche regionali.

![Distribuzione dello stato dei progetti]({{ site.baseurl }}/assets/images/eda/01_stato_progetto.png){: .img-fluid }

# La metrica: quando un progetto è a rischio {#metriche}

Il dataset non contiene un'etichetta di rischio: **la costruiamo noi**, e da qui in avanti è
l'unica misura che useremo. Tutti i tagli di questa pagina (territorio, dimensione, ciclo, tema,
regione) sono letti con lo stesso metro.

<div class="def-box">
  <p class="def-box__label">La nostra variabile chiave (e target del modello)</p>
  <h4>Quando un progetto è «a rischio»?</h4>
  <p>La costruiamo in modo conservativo, da due condizioni osservabili alla data di riferimento
  dei dati: il <strong>31 dicembre 2025</strong>, lo snapshot a cui è aggiornato il dataset
  OpenCoesione. <code>A_RISCHIO = 1</code> se il progetto:</p>
  <p><strong>1 · non è mai partito</strong>: stato «non avviato», qualunque sia la sua data
  prevista di fine (16.261 progetti, 7,9%), <em>oppure</em><br>
  <strong>2 · è in corso fuori tempo massimo</strong>: stato «in corso» con data di fine
  prevista anteriore alla data di riferimento (51.237 progetti, 24,8%).</p>
  <p>In totale: <strong>67.498 progetti, il 32,6%</strong>.</p>
  <p class="def-box__note">Due esclusioni deliberate: i progetti <em>conclusi</em> in ritardo non
  contano (la metrica guarda chi è ancora per strada, non chi è arrivato tardi) e i
  <em>liquidati</em> sono una categoria a parte. È la fotografia di un istante: un progetto oggi
  a rischio può ancora concludersi: per questo «a rischio», non «fallito».</p>
</div>

Le **due componenti** non descrivono lo stesso problema, e le teniamo separate ogni volta che
dicono qualcosa. Un progetto **mai avviato** è un problema di partenza: i fondi sono assegnati e
fermi. Un progetto **fuori tempo massimo** è un problema di esecuzione: è partito e non chiude.
In aggregato domina il secondo (24,8% contro 7,9%), ma il rapporto si ribalta a seconda di dove
si guarda, e sono proprio quei ribaltamenti a dire qualcosa.

# Divario territoriale (Nord / Sud) {#divario}

È il cuore del progetto, ed è netto: nel Mezzogiorno è a rischio il **42,0%** dei progetti contro
il **20,5%** del Centro-Nord. Oltre il doppio, ventuno punti di distanza.

Il dato più interessante, però, è **dove** sta il divario. Sui progetti **mai avviati** le due aree
sono quasi pari, e con il segno rovesciato rispetto all'attesa: **8,8%** al Centro-Nord contro
**7,2%** al Sud. Tutto il divario sta nella seconda componente, i progetti **fuori tempo massimo**:
**11,7% contro 34,8%**, tre volte tanto. Al Sud i progetti partono quanto al Nord: è tenerli in
corsa che non riesce. Il problema non è l'assegnazione dei fondi, è la loro gestione.

![Esiti per macroarea territoriale]({{ site.baseurl }}/assets/images/eda/04_territorio.png){: .img-fluid }

Va detto che il Mezzogiorno gestisce molti più fondi (**215 contro 79 mld €**): è coerente con la
missione redistributiva della politica di coesione, e per questo il confronto va sempre letto in
percentuale, mai in valore assoluto.

Un divario così grande potrebbe però essere solo un effetto di composizione: se il ciclo più recente
(appena partito) pesasse di più al Sud, il gap sarebbe un artefatto. Lo verifichiamo **dentro ogni
ciclo**, e il risultato regge: in *tutti* i cicli il Mezzogiorno è più a rischio, con uno scarto che
va da **+12,3** punti (2021-2027) a **+30,0** (2014-2020). Il divario è **persistente**: non dipende
dal calendario dei cicli. Il ciclo, però, è solo una delle composizioni possibili: resta da pesare
quella per **dimensione** e tema, perché i progetti grandi si inceppano di più ovunque e se al Sud
pesassero di più, parte del gap potrebbe spiegarsi così. Quanto conta il territorio *in sé* lo misura
la [regressione multivariata]({{ site.baseurl }}/regressione.html).

<!-- TODO: incrocio macroarea × classe di importo. Se il divario regge dentro ogni classe,
     il claim si rafforza già in descrittiva. -->

![Divario di rischio Nord-Sud, per ciclo]({{ site.baseurl }}/assets/images/eda/07_divario_per_ciclo.png){: .img-fluid }

## Dove passano i fondi

Le barre dicono *quanto*, ma non mostrano il **percorso** dei soldi. Il diagramma di Sankey qui sotto
lo rende esplicito: ogni flusso ha uno spessore proporzionale ai fondi pubblici netti (in miliardi di €),
dalla **fonte** al **territorio** al **tema**. È una versione esatta all'euro, ricostruita dalla
scomposizione reale per fonte (FESR, FSE, FSC, Fondo di rotazione, PAC, Regione). La lettura chiave:
al Sud la coesione è più **nazionale (FSC)** che **europea (FESR)**, e i **trasporti** sono il tema
che assorbe la fetta maggiore.

<iframe src="{{ site.baseurl }}/assets/charts/plotly/sankey_fondi.html"
        title="Diagramma di Sankey dei fondi"
        style="width: 100%; height: 520px; border: none;"
        loading="lazy"></iframe>

<div style="margin: 0.5rem 0 1.5rem;">
  <p style="margin-bottom: 0.6rem;">I fondi della coesione arrivano da <strong>due famiglie</strong>: quelli
  <strong>europei</strong> (stanziati dall'UE) e quelli <strong>nazionali</strong> (messi dallo Stato
  italiano e dalle Regioni). Ecco cosa rappresenta ogni colore del diagramma.</p>
  <div style="display: flex; flex-wrap: wrap; gap: 0.6rem 1.4rem;">
    <div style="flex: 1 1 300px; min-width: 260px;">
      <p style="font-weight: 700; text-transform: uppercase; font-size: 0.8rem; letter-spacing: .04em; color: #555; margin-bottom: 0.4rem;">Fondi europei</p>
      <p style="margin: 0 0 0.5rem;"><span style="display:inline-block;width:12px;height:12px;background:#177E89;border-radius:2px;margin-right:6px;"></span><strong>FESR (UE)</strong>: Fondo Europeo di Sviluppo Regionale. Il principale fondo UE: infrastrutture, imprese, innovazione e ambiente.</p>
      <p style="margin: 0 0 0.5rem;"><span style="display:inline-block;width:12px;height:12px;background:#4FA7B1;border-radius:2px;margin-right:6px;"></span><strong>FSE (UE)</strong>: Fondo Sociale Europeo. Il fondo UE dedicato alle persone: lavoro, formazione e inclusione sociale.</p>
    </div>
    <div style="flex: 1 1 300px; min-width: 260px;">
      <p style="font-weight: 700; text-transform: uppercase; font-size: 0.8rem; letter-spacing: .04em; color: #555; margin-bottom: 0.4rem;">Fondi nazionali</p>
      <p style="margin: 0 0 0.5rem;"><span style="display:inline-block;width:12px;height:12px;background:#D1573B;border-radius:2px;margin-right:6px;"></span><strong>FSC (nazionale)</strong>: Fondo Sviluppo e Coesione. Il grande fondo <em>italiano</em> (non UE) contro i divari territoriali; al Sud è la voce più pesante.</p>
      <p style="margin: 0 0 0.5rem;"><span style="display:inline-block;width:12px;height:12px;background:#E1876B;border-radius:2px;margin-right:6px;"></span><strong>Fondo di rotazione (naz.)</strong>: la quota di cofinanziamento che lo Stato affianca ai programmi europei (L. 183/1987).</p>
      <p style="margin: 0 0 0.5rem;"><span style="display:inline-block;width:12px;height:12px;background:#A83E27;border-radius:2px;margin-right:6px;"></span><strong>PAC (nazionale)</strong>: Programma di Azione e Coesione. Risorse nazionali complementari ai programmi UE.</p>
      <p style="margin: 0 0 0.5rem;"><span style="display:inline-block;width:12px;height:12px;background:#8c6bb1;border-radius:2px;margin-right:6px;"></span><strong>Regione/locale</strong>: cofinanziamento messo direttamente da Regioni ed enti locali.</p>
      <p style="margin: 0 0 0.5rem;"><span style="display:inline-block;width:12px;height:12px;background:#bdbdbd;border-radius:2px;margin-right:6px;"></span><strong>Altro pubblico</strong>: altre fonti pubbliche senza voce dedicata (comuni, province, completamenti): fa quadrare i totali.</p>
    </div>
  </div>
  <p style="margin-top: 0.6rem; font-size: 0.88rem; color: #666;">I due nodi centrali del diagramma,
  Centro-Nord e Mezzogiorno, usano i colori dedicati al territorio (viola e oro) e non quelli delle
  metriche: in queste pagine l'arancio significa «rischio», e un territorio non è un esito.</p>
</div>

# Dimensione, ciclo e tema

Tre tagli aiutano a capire *chi* si inceppa e *chi* no.

**Dimensione.** Il rischio non cresce all'infinito con la taglia del progetto: disegna una
**campana**. Sale dal 29,4% dei progetti piccoli fino al **43,9% della fascia 5-10 milioni**, poi
ridiscende (42,9% fra 10 e 50 milioni, 38,5% sopra i 50). Il punto critico non sono i progetti
giganti ma quelli **medio-grandi**: abbastanza complessi da incepparsi, non abbastanza grandi da
essere seguiti uno per uno.

![Percentuale di progetti a rischio per classe di importo]({{ site.baseurl }}/assets/images/eda/05_dimensione_rischio.png){: .img-fluid }

Resta un dato di peso da tenere presente: i progetti piccoli (100-500k) sono il 70% del totale
ma circa 31 dei 315 miliardi, mentre i 623 progetti sopra i 50 milioni ne valgono da soli 120.
Contare i progetti e pesarli per importo sono due letture diverse, ed entrambe vanno dichiarate.

**Ciclo.** Qui il risultato è controintuitivo: il ciclo peggiore non è quello appena partito, è il
**2014-2020 con il 38,5%**, sopra il 2021-2027 fermo al 36,8%. Il ciclo che a questo punto dovrebbe
essere in chiusura è quello con la quota più alta di progetti fermi o fuori tempo massimo. I due
cicli chiusi restano molto sotto: 21,8% e 25,6%.

E la scomposizione mostra che i due cicli in coda hanno problemi **opposti**. Nel 2021-2027 il
rischio è quasi tutto «mai avviati» (**34,7%** su 36,8): fondi assegnati a progetti non ancora
partiti, il che per un ciclo di due anni è in buona parte fisiologico. Nel 2014-2020 succede il
contrario: i mai avviati sono il **3,5%** e il **35,0%** è «fuori tempo massimo», cioè progetti
partiti che a fine 2025 avevano già sforato la scadenza. Sommarli in un unico numero li avrebbe
fatti sembrare la stessa cosa.

![Percentuale di progetti a rischio per ciclo di programmazione]({{ site.baseurl }}/assets/images/eda/06_ciclo_rischio.png){: .img-fluid }

Una cautela sul 2021-2027: è un dato **censurato**. Molti dei suoi progetti hanno ancora una
scadenza davanti, quindi non possono essere a rischio per definizione, e quella percentuale può
solo salire.

**Tema.** Il tema più esposto è la **competitività delle imprese** (39,6% a rischio), seguito da
**trasporti e mobilità** (37,4%) e **ambiente** (35,2%). All'estremo opposto reti e servizi digitali
(21,8%), energia (24,2%) e capacità amministrativa (26,2%). I trasporti meritano attenzione perché
muovono i fondi maggiori, quasi **100 miliardi su 315**: un tasso sopra la media su un terzo di tutto
il denaro non è un dettaglio settoriale.

![Rischio per tema]({{ site.baseurl }}/assets/images/eda/09_tema.png){: .img-fluid }

# La mappa regionale

Portando il tasso a livello regionale, il gradiente Nord→Sud si conferma, ma con eccezioni in
**entrambe** le direzioni, ed è la ragione per cui vale la pena guardarla e non fermarsi alle due
macroaree.

In coda c'è la **Sicilia** con il **53,8%**, staccata di tredici punti dalla seconda: più di un
progetto su due. Seguono Campania (40,5%), Calabria (39,8%) e Puglia (38,5%). In testa la **Liguria**
con il **9,2%**, poi Valle d'Aosta (15,5%), Molise (16,5%) e Veneto (16,6%).

Le eccezioni. Nel Centro-Nord, **Marche** (31,4%) e **Lazio** (27,6%) stanno peggio di quattro
regioni del Mezzogiorno: nel caso delle Marche il motivo si legge nella scomposizione, perché il
**16,2%** dei loro progetti non è mai partito, il valore più alto d'Italia, mentre il 15,2% fuori
tempo è nella norma del Nord. Dall'altro lato il **Molise** sta davanti a Lombardia, Piemonte e
Veneto. Il territorio spiega molto, ma non tutto: chi amministra conta.

La dashboard qui sotto è interattiva. Il menu a tendina sceglie **quale vista del rischio** mostrare:
il totale, la sola quota di progetti mai avviati o la sola quota fuori tempo massimo. La mappa si
ricolora e la classifica regionale si aggiorna; passando il mouse su una regione la si evidenzia in
entrambe le viste. Cambiando voce si vede che le regioni non si dispongono nello stesso ordine, ed è
il punto: due regioni con lo stesso rischio complessivo possono avere problemi opposti.

<div style="width: 100vw; margin-left: calc(50% - 50vw); display: flex; justify-content: center; margin-top: 2.5rem; margin-bottom: 1.5rem;">
  <iframe src="{{ site.baseurl }}/assets/charts/interactive/dashboard_regioni.html"
          title="Dashboard interattiva delle regioni"
          style="width: min(960px, 96vw); height: 720px; border: none; transform: translateX(30px);"
          loading="lazy"></iframe>
</div>

# Due approfondimenti

**Tempi di esecuzione.** Ogni progetto ha una fase di "esecuzione", non solo le opere: per un
lavoro pubblico è il cantiere, per un incentivo è la realizzazione dell'investimento da parte
dell'impresa, con rendicontazione ed erogazione a tranche. La sorpresa è che la fase più lunga non
è quella dei cantieri (~610 giorni) ma quella degli **incentivi alle imprese** (~840); l'acquisto
di beni è il più rapido (~410). Attenzione però a non leggere le durate come ritardi: i piani di
investimento sono spesso pluriennali per costruzione. Resta il fatto che i tempi lunghi non
abitano solo nei cantieri.

![Durata della fase di esecuzione per natura del progetto]({{ site.baseurl }}/assets/images/eda/11_fase_esecuzione.png){: .img-fluid }

**Governance e ritardi.** Un'ipotesi diffusa è che più enti coinvolti significhino più ritardi.
Sui nostri dati la correlazione è praticamente nulla (≈ −0,04): questa vista descrittiva **non** la
sostiene. Va letta con prudenza (il ritardo è misurato quasi solo sui progetti conclusi): il test
pulito è quello della [regressione multivariata]({{ site.baseurl }}/regressione.html#odds-ratio), dove il
numero di enti entra tra i predittori sul *rischio* (che include anche i progetti mai partiti):
l'esito è **odds ratio 0,96**: a parità di dimensione, tema, tipo di intervento, fonte di
finanziamento e territorio, più enti non significano più rischio. Ipotesi archiviata.

![Numero di enti e ritardo medio]({{ site.baseurl }}/assets/images/eda/12_governance.png){: .img-fluid }

# Correlazioni {#correlazioni}

Prima di passare al modello serve capire quali variabili portano informazione davvero diversa. La
prima matrice mette a confronto tutte le variabili numeriche continue e fa emergere **tre gruppi
ridondanti**: le grandezze finanziarie assolute (finanziamento, pagamenti, costo realizzato, con
correlazioni fino a 0,90), i due contatori di governance (numero di attuatori e numero di enti, di
fatto la stessa variabile: 0,98) e le quote UE e Stato, quasi complementari per costruzione (−0,72).
Da ciascun gruppo il modello prenderà una variabile sola, per non contarne due volte la stessa cosa.

Il rischio resta fuori dalla griglia: è una variabile binaria, e i suoi coefficienti non sarebbero
confrontabili con quelli calcolati tra variabili continue. Il suo legame con le altre variabili si
legge nei tassi per gruppo di questa pagina e nella regressione.

![Matrice di correlazione di tutte le variabili continue]({{ site.baseurl }}/assets/images/eda/10_correlazione.png){: .img-fluid }

Tenendo una variabile per gruppo, e scartando tutto ciò che si osserva solo **dopo** l'avvio del
progetto (pagamenti, assorbimento, ritardi: sono misure di esito, non condizioni di partenza), resta
un nucleo di quattro variabili note fin dal **giorno zero**: importo, quota di fondi europei, numero
di enti e quota di capitale privato. Da qui partono le analisi successive, che usano tutte e quattro
lo stesso insieme: il clustering le prende così come sono, la
[regressione]({{ site.baseurl }}/regressione.html#matrice) e il Random Forest usano l'importo in
fasce e le altre tre invariate.

![Matrice di correlazione delle sole variabili note alla partenza]({{ site.baseurl }}/assets/images/eda/10c_correlazione_ripulita.png){: .img-fluid }

La seconda matrice serve a verificare che l'operazione sia riuscita, e il risultato è netto: fuori
dalla diagonale la correlazione più alta è **0,20**. Le quattro variabili raccontano cose diverse, e
i coefficienti del modello si potranno leggere uno per uno senza il sospetto che si stiano rubando
informazione a vicenda.

# In sintesi

Un progetto su tre (**32,6%**) è a rischio, e in aggregato il problema è l'esecuzione più che
l'avvio: il 24,8% è partito e ha già sforato la scadenza, il 7,9% non è mai partito. Il rischio si
concentra sui progetti **medio-grandi** (picco del 43,9% fra 5 e 10 milioni) e sul ciclo
**2014-2020** (38,5%), non su quello appena partito.

Il **divario territoriale** è netto (42,0% contro 20,5%) e resiste al controllo per ciclo. E ha una
forma precisa: non sta nei progetti mai avviati, dove le due aree sono pari, ma in quelli che partono
e non chiudono. La complessità di governance, invece, **non** spiega i ritardi.

Restano due avvertenze prima di trarre conclusioni causali: le differenze descrittive non bastano, e
le analisi sui ritardi coprono solo la parte di progetti con una fine effettiva. Per questo il passo
successivo è la [**regressione multivariata**]({{ site.baseurl }}/regressione.html), che stima il
peso del territorio a parità di dimensione, tema, tipo di intervento e fonte di finanziamento.

<hr>

<p style="font-size: 0.8rem; color: #888; margin-top: 1.5rem;">
  Immagine di copertina: <a href="https://unsplash.com/it/@upmanis" target="_blank" rel="noopener">Kaspars Upmanis</a>, Matera, su <a href="https://unsplash.com" target="_blank" rel="noopener">Unsplash</a>.
</p>
