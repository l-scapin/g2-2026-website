---
layout: default
title: "Random Forest"
show_sidetoc: true
vega: true
header_type: hero #base, post, hero, image, splash
header_img: assets/images/hero_random_forest.jpg
header_img_position: center
header_title: "Random Forest"
subtitle: "Prevedere il rischio prima che si manifesti"
---

<!-- Numeri dal notebook 04 (Random Forest + SHAP), verificati rieseguendo il modello. -->

<div class="full-width-wrapper">
    <img src="{{ site.baseurl }}/assets/images/header.svg" alt="sbd-pattern" class="full-width-image">
</div>

La [regressione]({{ site.baseurl }}/regressione.html) ha risposto a una domanda precisa: **quanto pesa ciascun fattore** sul ritardo di un progetto, a parità di tutte le altre condizioni. Ma ne resta una altrettanto concreta per chi deve gestire i fondi: **è possibile prevedere prima del via quali progetti rischiano di incepparsi, così da monitorarli più da vicino?**

Per rispondere abbiamo messo alla prova i dati con un **Random Forest**, un algoritmo che non si limita a "pesare" le singole variabili, ma cerca in autonomia migliaia di combinazioni e soglie critiche nascoste nei dati. 
{: .lead }

# Spiegare contro indovinare: perché due modelli

Non è una gara a chi ha l'algoritmo migliore, ma una divisione dei compiti. I due modelli rispondono a domande diverse.

La **regressione logistica** serve a *spiegare*. Ci restituisce un numero esatto per ogni fattore: ci dice ad esempio che, a parità di tutto il resto, fare un progetto al Sud triplica le probabilità di rischio. È trasparente e rigorosa, ma ha una struttura rigida.

Il **Random Forest** serve a *prevedere*. Costruisce centinaia di alberi decisionali su frammenti di dati diversi e li fa "votare" per decidere se un nuovo progetto finirà fuori strada. È potentissimo nel catturare interazioni complesse (ad esempio: cosa succede se un progetto è enorme, al Sud, ma finanzia solo acquisti di beni?), ma è una "scatola nera" che non produce coefficienti semplici da leggere. 

Perché il confronto sia leale, il Random Forest ha ricevuto in pasto **le stesse identiche informazioni** della regressione (territorio, tipo di intervento, tema, dimensione, quota di fondi europei e privati, numero di enti) ed è stato valutato solo su progetti che non aveva **mai visto prima** durante la fase di addestramento.

# Il risultato: una previsione solida e onesta

Il primo modello addestrato ha raggiunto un'affidabilità predittiva (misurata tramite l'indice AUC, dove 0,5 è il caso e 1 è la previsione perfetta) apparentemente eccellente, pari a **0,813**. Tuttavia, interrogando la *black box* del modello, abbiamo notato un'anomalia: la variabile `QUOTA_UE` aveva un peso sospettosamente alto sulle decisioni dell'algoritmo. Indagando su questo indizio, abbiamo capito il perché: l'algoritmo stava sfruttando l'esatto numero di cifre decimali di quella percentuale come una sorta di "codice a barre" per riconoscere il singolo piano di finanziamento, e di conseguenza lo specifico bando amministrativo. In pratica, il modello non stava valutando il rischio intrinseco del progetto, ma "barava" riconoscendo la scrivania di partenza.

Per verificare e correggere questo effetto, abbiamo "sfocato" i dati arrotondando le quote finanziarie, nascondendo l'impronta digitale del bando. A questo punto l'AUC si è assestata a **0,778**:

| Dati a disposizione del modello | Affidabilità della previsione (AUC) |
|---|---|
| Quote esatte (effetto "codice a barre") | 0,813 |
| **Quote arrotondate (il modello reale)** | **0,778** |
| Regressione logistica (per confronto) | 0,668 |

L'affidabilità è fisiologicamente diminuita — confermando che l'effetto "bando" esisteva ed inquinava il dato — ma resta comunque un risultato estremamente buono e nettamente superiore a quello della regressione (0,668). **Questo 0,778 è il valore reale, onesto e robusto della nostra capacità predittiva.** 

Per un *policy maker* o un gestore di fondi, questo significa che creare un modello predittivo al "giorno zero" è assolutamente possibile e utile, a patto di prestare un'estrema attenzione critica per disinnescare dinamiche algoritmiche nascoste come questa.

# Dentro la scatola nera: l'impatto dei fattori {#shap}

Per evitare di avere un modello che lancia allarmi senza dirci il perché, abbiamo "aperto" il Random Forest usando un metodo di *explainable AI* (chiamato **SHAP**) in grado di calcolare quanto ogni singola caratteristica ha spinto la previsione di un progetto verso il successo o verso il baratro.

{% include altair.html id="vis-riepilogo-impatto" file="/assets/charts/vis_riepilogo_impatto.json" %}

Questo grafico offre la panoramica globale su cosa orienta l'algoritmo. Innanzitutto, le variabili sono **ordinate dall'alto verso il basso per importanza globale**: in cima c'è il territorio, seguito dalla quota di fondi europei, dalla natura dell'intervento e dal tema. Il modello conferma le stesse esatte priorità della regressione.

In secondo luogo, le scatole mostrano l'**intensità (o magnitudo) dell'impatto**. È importante fare una distinzione: mentre per le variabili binarie (come il Territorio) è possibile dedurre una direzione generale chiara, per le variabili multiclasse (come Tema e Natura) il grafico mette tutto insieme e ci dice semplicemente *quanto è forte* l'effetto di quella caratteristica sulle scelte del modello. Per scoprire la **direzione specifica** — ovvero se l'acquisto di beni o i lavori pubblici spingano la probabilità di rischio in alto o in basso — si rimanda ai grafici di dettaglio della sezione successiva.

# L'identikit confermato: il dettaglio variabile per variabile 

Se il grafico precedente ci dà la classifica dell'importanza, i focus qui sotto scendono nel dettaglio per mostrarci **quali specifici valori** spingono verso il ritardo o verso la sicurezza. La logica visiva è la medesima: la scatola colorata racchiude il cuore dei progetti (il 50% centrale della distribuzione), mentre la linea rossa fissa la soglia di rischio zero. A destra il fattore aumenta l'allarme, a sinistra lo riduce.

## Il peso della geografia 

{% include altair.html id="vis-territorio" file="/assets/charts/vis_territorio.json" %}

Il territorio non ammette sfumature e mostra **due distribuzioni nettamente separate**. I progetti del Mezzogiorno (color oro) si collocano abbondantemente a destra, confermandosi il bacino di rischio principale. Quelli del Centro-Nord (in viola) si posizionano tutti a sinistra, nell'area di sicurezza. È la stessa spaccatura individuata dalla regressione: due modelli matematicamente opposti confermano l'esatta, identica tendenza.

## Il vincolo dei fondi europei 

{% include altair.html id="vis-quota-ue" file="/assets/charts/vis_quota_ue.json" %}

Nel paragrafo precedente abbiamo visto come i decimali della quota europea rischiassero di fare da "codice a barre". Ma se sintetizziamo i risultati raggruppando i progetti in base alla sola presenza o assenza di fondi UE, emerge una dinamica strutturale chiara: disporre di fondi europei (in verde) tende a spingere la distribuzione verso l'area di sicurezza, sotto lo zero. Come già rilevato dalla regressione logistica, le scadenze vincolanti e le rigide regole di disimpegno europee agiscono da forte disincentivo ai ritardi, a prescindere dall'importo esatto.

## Cosa si fa con i soldi: la natura dell'intervento {#dip-natura}

{% include altair.html id="vis-natura" file="/assets/charts/vis_natura.json" %}

È il segnale più inequivocabile. L'**acquisto di beni** è l'unica operazione che il modello considera sistematicamente sicura (tutta la distribuzione è sotto lo zero). All'estremo opposto, **erogare contributi ad altri soggetti** o realizzare **lavori pubblici** spinge drammaticamente verso l'alto l'allarme rischio. Ancora una volta, la "direzione" appresa dal Random Forest è perfettamente in linea con quanto ci diceva la regressione.

## Di cosa si parla: il tema 

{% include altair.html id="vis-tema" file="/assets/charts/vis_tema.json" %}

Anche qui l'identikit regge. Spingono verso l'area di rischio i progetti legati alla **competitività delle imprese**, all'**istruzione** e all'**occupazione**. Agiscono invece da scudo l'**ambiente**, l'**energia** e le **reti digitali**. Rispetto alla regressione, qui notiamo un dettaglio in più: l'estensione orizzontale per ogni tema è molto ampia e attraversa quasi sempre lo zero. Significa che il tema, da solo, non è una condanna automatica, ma interagisce fortemente con il resto del progetto.

## Quanto si spende: la dimensione 

{% include altair.html id="vis-dimensione" file="/assets/charts/vis_dimensione.json" %}

I progetti più piccoli (da 100 a 500 mila euro) sono l'unico gruppo prevalentemente al riparo. Salendo con i fondi, il rischio cresce fino a toccare il suo apice per i progetti **medio-grandi (tra 1 e 10 milioni di euro)**, per poi ridiscendere leggermente sui mega-progetti. È l'esatta forma "a campana" che avevamo già osservato esplorando i dati base.

# Conclusioni 

**Costruire un sistema di allerta predittivo è possibile e utile.** Ripulendo i dati dalle illusioni statistiche e utilizzando unicamente informazioni note al momento della firma, è possibile ottenere una previsione robusta (0,778 AUC). Per un *policy maker*, questo significa avere in mano una bussola: non serve a scartare o definanziare i progetti, ma a definire su chi attivare un tutoraggio mirato e un monitoraggio stretto prima che gli iter si blocchino.

**Il punto di forza: catturare le combinazioni complesse.** A differenza della regressione, il Random Forest non valuta i fattori in modo isolato: riesce a cogliere da solo le interazioni a coppie o di gruppo (ad esempio come il rischio di un certo tipo di intervento cambi radicalmente a seconda del territorio in cui si localizza). I valori SHAP ci permettono di "aprire la scatola nera" e verificare che queste combinazioni abbiano un senso logico.

**Due strumenti per due scopi diversi.** Quando le due metodologie concordano sui fattori principali (Mezzogiorno, contributi a soggetti terzi, fasce dimensionali medio-grandi), il dato diventa inoppugnabile. La scelta tra i due dipende unicamente dall'obiettivo: se vogliamo **anticipare il rischio** intercettando chi si incepperà, lo strumento ideale è il **Random Forest**; se invece l'obiettivo pubblico è capire il peso netto e la **causalità isolata** di una singola leva normativa a parità del resto, il riferimento è l'Odds Ratio della **regressione**.

