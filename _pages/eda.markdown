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
subtitle: "Qualità dei dati, le tre metriche di esito e i primi pattern"
---

<div class="full-width-wrapper">
    <img src="{{ site.baseurl }}/assets/images/header.svg" alt="sbd-pattern" class="full-width-image">
</div>

Prima di modellare qualsiasi cosa, guardiamo i dati. Lavoriamo su **206.777 progetti**
della politica di coesione italiana (fonte: dati aperti **OpenCoesione**, solo progetti da
almeno 100.000 € e pubblicati). L'esplorazione è organizzata sulle nostre tre domande:
i progetti **si concludono**? Sono **a rischio**? Fondi ed esiti sono **equi tra Nord e Sud**?
{: .lead }

# Qualità e preparazione dei dati

Il dataset non ha righe duplicate: ogni progetto è identificato in modo univoco dalla coppia
CUP + codice locale. I valori mancanti ci sono, ma quasi tutti sono *strutturali*, non errori.
Per esempio, il ritardo e la data di fine effettiva mancano sui progetti non ancora conclusi,
semplicemente perché una fine non c'è ancora. Le descrizioni tematiche e il fondo europeo mancano
invece sui progetti a finanziamento puramente nazionale (FSC, PAC): anche questo è atteso, non un buco.

![Valori mancanti per colonna]({{ site.baseurl }}/assets/images/eda/02_missing.png){: .img-fluid }

Prima di ogni analisi fine teniamo a mente due trappole nei dati: alcuni pagamenti sono
**negativi** (rettifiche contabili, pochi ma da azzerare nelle somme), e circa l'1% dei progetti è
**multi-regione**, con i nomi delle regioni concatenati da `:::`, e vanno esclusi prima di
costruire mappe o classifiche regionali.

![Distribuzione dello stato dei progetti]({{ site.baseurl }}/assets/images/eda/01_stato_progetto.png){: .img-fluid }

# Le tre metriche di esito {#metriche}

Riassumiamo l'esito di ogni progetto con tre misure semplici. **Concluso**: il progetto risulta
chiuso. **A rischio**: la nostra variabile chiave, definita nel box qui sotto. **Tasso di
assorbimento**: quanto è stato effettivamente pagato rispetto al finanziamento pubblico (da 0 a 2,
dove valori sopra 1 segnalano un forte cofinanziamento privato).

<div class="def-box">
  <p class="def-box__label">La nostra variabile chiave (e target del modello)</p>
  <h4>Quando un progetto è «a rischio»?</h4>
  <p>Il dataset non contiene un'etichetta di rischio: <strong>la costruiamo noi</strong>, in modo
  conservativo, da due condizioni osservabili alla data di riferimento dei dati: il <strong>31 dicembre 2025</strong>, lo snapshot a cui è aggiornato il dataset OpenCoesione.
  <code>A_RISCHIO = 1</code> se il progetto:</p>
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

Nel complesso circa **metà** dei progetti è conclusa e quasi un terzo (**32,6%**) è a rischio. L'assorbimento merita
attenzione: la sua distribuzione è **bimodale**, con tanti progetti fermi a 0 e un grande picco
intorno a 1 (spesa completa). La media (0,72) da sola dice poco: va sempre letta insieme allo stato e al ciclo.

![Distribuzione del tasso di assorbimento]({{ site.baseurl }}/assets/images/eda/03_assorbimento_dist.png){: .img-fluid }

# Divario territoriale (Nord / Sud) {#divario}

È il cuore del progetto. Confrontando Centro-Nord e Mezzogiorno il divario è netto: il Centro-Nord
conclude il **58,8%** dei progetti contro il **41,6%** del Sud, ed è a rischio molto meno
(**20,5% vs 42,0%**). Sull'assorbimento la distanza è più contenuta (**0,75 vs 0,69**). Va detto che
il Mezzogiorno gestisce molti più fondi (**215 vs 79 mld €**): è coerente con la missione redistributiva
della politica di coesione.

![Esiti per macroarea territoriale]({{ site.baseurl }}/assets/images/eda/04_territorio.png){: .img-fluid }

Un divario così grande potrebbe però essere solo un effetto di composizione: se il ciclo più recente
(appena partito, quindi con pochi conclusi) pesasse di più al Sud, il gap sarebbe un artefatto.
Lo verifichiamo **dentro ogni ciclo**, e il risultato regge: in *tutti* i cicli il Centro-Nord
conclude di più. Il divario è **persistente**: non dipende dal calendario dei cicli. Il ciclo, però,
è solo una delle composizioni possibili: resta da pesare quella per **dimensione** e tema, perché
i progetti grandi concludono meno ovunque e se al Sud pesassero di più, parte del gap potrebbe
spiegarsi così. Quanto conta il territorio *in sé* lo misura la
[regressione multivariata]({{ site.baseurl }}/regressione.html).

<!-- TODO: incrocio macroarea × classe di importo. Se il divario regge dentro ogni classe,
     il claim si rafforza già in descrittiva. -->

![Divario di conclusione Nord-Sud, per ciclo]({{ site.baseurl }}/assets/images/eda/07_divario_per_ciclo.png){: .img-fluid }

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
</div>

# Dimensione, ciclo e tema

Tre tagli aiutano a capire *chi* conclude e *chi* no.

**Dimensione.** Il rischio non cresce all'infinito con la taglia del progetto: disegna una
**campana**. Sale dal 29,4% dei progetti piccoli fino al **43,9% della fascia 5-10 milioni**, poi
ridiscende (38,5% sopra i 50 milioni). Il punto critico non sono i progetti giganti ma quelli
**medio-grandi**: abbastanza complessi da incepparsi, non abbastanza grandi da essere seguiti uno
per uno.

![Percentuale di progetti a rischio per classe di importo]({{ site.baseurl }}/assets/images/eda/05_dimensione_rischio.png){: .img-fluid }

La conclusione racconta invece una storia monotona (dal 53,6% dei piccoli al 13,8% degli oltre 50
milioni, con l'assorbimento che scende da 0,75 a 0,42), ma va letta con una cautela: i progetti
giganti sono concentrati nei cicli più recenti, quindi parte di quel calo è semplicemente meno
tempo a disposizione. Resta un dato di peso: i progetti piccoli (100-500k) sono il 70% del totale
ma circa il 10% dei fondi, mentre i 623 progetti sopra i 50 milioni valgono da soli 120 miliardi.
I risultati vanno pesati per importo, non solo contati.

**Ciclo.** Qui il confronto fra le due metriche è il risultato. Guardando i **conclusi** si legge
solo l'età del ciclo: i cicli chiusi sono al 76% e al 66%, il 2014-20 a metà, il 2021-2027 appena
iniziato al 5%. È quasi una tautologia. Guardando il **rischio** emerge invece qualcosa che non ci
si aspetta: il ciclo peggiore non è quello appena partito, è il **2014-2020 con il 38,5%**, sopra
il 2021-2027 fermo al 36,8%. Il ciclo che a questo punto dovrebbe essere in chiusura è quello con
la quota più alta di progetti fermi o fuori tempo massimo.

![Percentuale di progetti a rischio per ciclo di programmazione]({{ site.baseurl }}/assets/images/eda/06_ciclo_rischio.png){: .img-fluid }

Una cautela sul 2021-2027: è un dato **censurato**. Molti dei suoi progetti hanno ancora una
scadenza davanti, quindi non possono essere a rischio per definizione, e quella percentuale può
solo salire.

**Tema.** "Competitività delle imprese" è il tema che conclude meno (37%) e assorbe meno (0,57);
vanno meglio digitale, energia e occupazione. I "trasporti" muovono i fondi maggiori (~100 mld) ma
concludono poco (46%): un'area da tenere d'occhio.

![Esiti per tema]({{ site.baseurl }}/assets/images/eda/09_tema.png){: .img-fluid }

# La mappa regionale

Portando i tassi a livello regionale, il gradiente Nord→Sud si conferma quasi senza eccezioni:
in coda Sicilia (31% concluso, 54% a rischio), con Lazio, Calabria e Campania subito sopra;
in testa Liguria (76%), Molise e Piemonte. La dashboard qui sotto è interattiva: con il menu a tendina scegli la metrica
(completamento, rischio o assorbimento), la mappa si ricolora e la classifica regionale si aggiorna;
passando il mouse su una regione la evidenzi in entrambe le viste.

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

Gli esiti (concluso, a rischio) restano fuori dalla griglia: sono variabili binarie, e i loro
coefficienti non sarebbero confrontabili con quelli calcolati tra variabili continue. Il loro legame
con le altre variabili si legge nei tassi per gruppo di queste pagine e nella regressione.

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

I progetti si concludono a metà, con forte dipendenza dall'età del ciclo e dalla dimensione: i grandi
concludono molto meno. Il rischio (32,6%) si concentra sui progetti **medio-grandi** (picco del 43,9%
fra 5 e 10 milioni) e sul ciclo **2014-2020** (38,5%), non su quello appena partito.
Il **divario territoriale** è netto e resiste al controllo per ciclo (conclusione +17 punti, rischio
−21 a favore del Nord). La complessità di governance, invece, **non** spiega i ritardi.

Restano due avvertenze prima di trarre conclusioni causali: le differenze descrittive non bastano, e
le analisi sui ritardi coprono solo la parte di progetti con una fine effettiva. Per questo il passo
successivo è la [**regressione multivariata**]({{ site.baseurl }}/regressione.html), che stima il
peso del territorio a parità di dimensione, tema, tipo di intervento e fonte di finanziamento.

<hr>

<p style="font-size: 0.8rem; color: #888; margin-top: 1.5rem;">
  Immagine di copertina: <a href="https://unsplash.com/it/@upmanis" target="_blank" rel="noopener">Kaspars Upmanis</a>, Matera, su <a href="https://unsplash.com" target="_blank" rel="noopener">Unsplash</a>.
</p>
