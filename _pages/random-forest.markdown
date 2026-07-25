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

La [regressione]({{ site.baseurl }}/regressione.html) ha risposto a una domanda precisa: **quanto pesa ciascun fattore** sul ritardo di un progetto, a parità di tutte le altre condizioni. Ma ne resta una altrettanto concreta per chi deve gestire i fondi: se conosciamo: **è possibile prevedere prima del via quali progetti rischiano di incepparsi, così da monitorarli più da vicino?**

Per rispondere abbiamo messo alla prova i dati con un **Random Forest**, un algoritmo che non si limita a "pesare" le singole variabili, ma cerca in autonomia migliaia di combinazioni e soglie critiche nascoste nei dati. 
{: .lead }

# Spiegare contro indovinare: perché due modelli

Non è una gara a chi ha l'algoritmo migliore, ma una divisione dei compiti. I due modelli rispondono a domande diverse.

La **regressione logistica** serve a *spiegare*. Ci restituisce un numero esatto per ogni fattore: ci dice ad esempio che, a parità di tutto il resto, fare un progetto al Sud triplica le probabilità di rischio. È trasparente e rigorosa, ma ha una struttura rigida.

Il **Random Forest** serve a *prevedere*. Costruisce centinaia di alberi decisionali su frammenti di dati diversi e li fa "votare" per decidere se un nuovo progetto finirà fuori strada. È potentissimo nel catturare interazioni complesse (ad esempio: cosa succede se un progetto è enorme, al Sud, ma finanzia solo acquisti di beni?), ma è una "scatola nera" che non produce coefficienti semplici da leggere. 

Perché il confronto sia leale, il Random Forest ha ricevuto in pasto **le stesse identiche informazioni** della regressione (territorio, tipo di intervento, tema, dimensione, quota di fondi europei e privati, numero di enti) ed è stato valutato solo su progetti che non aveva **mai visto prima** durante la fase di addestramento.

# Il risultato: una previsione (fin troppo) accurata

Il Random Forest batte la regressione logistica con un margine ampissimo. Misurando l'affidabilità della previsione (tramite l'indice AUC, dove 0,5 è il caso e 1 è la previsione perfetta), il Random Forest **balza a 0,813**, lasciando la regressione indietro a **0,669**. 

Significa che prevedere l'esito di un progetto conoscendo solo la sua "carta d'identità" al giorno zero è assolutamente possibile. Ma da dove arriva un salto di qualità così netto? Analizzando il modello, scopriamo che la capacità predittiva aumenta notevolmente perché l'algoritmo impara a **riconoscere l'origine amministrativa dei fondi**, più che le caratteristiche intrinseche dei progetti.

La variabile che gli alberi usano di più per orientarsi è la **quota di fondi europei**. Questa percentuale, però, non è un numero a caso: i suoi decimali identificano in modo precisissimo il **piano di finanziamento**, e di conseguenza il bando e l'amministrazione che lo gestisce. Il modello ha semplicemente imparato che una certa combinazione di decimali corrisponde a un bando specifico, e che quel bando ha avuto un esito disastroso.

Per verificarlo, abbiamo tolto gli "occhiali da vista" all'algoritmo, arrotondando le percentuali per nascondere i decimali identificativi:

| Dati a disposizione del modello | Affidabilità della previsione (AUC) |
|---|---|
| Quote esatte (con tutti i decimali) | **0,813** |
| Quote arrotondate al 10% | 0,778 |
| Regressione logistica (per confronto) | 0,669 |

La lettura è duplice. **Il vantaggio del Random Forest è reale**: anche "sfocando" le variabili finanziarie, l'affidabilità resta alta (0,778), a conferma che le combinazioni trovate dall'algoritmo sono solide. Ma per chi deve prendere decisioni politiche, questo è un avvertimento vitale: quando chiediamo a un modello predittivo di stimare il rischio, rischiamo che impari a riconoscere **da quale scrivania** è partito il progetto, non **com'è fatto**.

# Dentro la scatola nera: l'impatto dei fattori {#shap}

Per evitare di avere un modello che lancia allarmi senza dirci il perché, abbiamo "aperto" il Random Forest usando un metodo (chiamato **SHAP**) in grado di calcolare quanto ogni singola caratteristica ha spinto la previsione di un progetto verso il successo o verso il baratro.

{% include altair.html id="vis-riepilogo-impatto" file="/assets/charts/vis_riepilogo_impatto.json" %}

Questo grafico offre la panoramica globale su cosa orienta l'algoritmo e si legge in due modi. Innanzitutto, le variabili sono **ordinate dall'alto verso il basso per importanza**: in cima c'è il territorio, seguito dalla quota di fondi europei, dalla natura dell'intervento e dal tema. 

In secondo luogo, le scatole mostrano la **direzione dell'impatto**: la linea tratteggiata rossa segna lo zero. A destra (valori positivi) si trovano i casi in cui la variabile spinge verso il rischio, a sinistra quelli in cui lo riduce. Variabili come il territorio o la quota europea mostrano una "forbice" molto ampia, capace di spostare la previsione in modo radicale. 

# L'identikit confermato: il dettaglio variabile per variabile {#dipendenze}

Se il grafico precedente ci dà la classifica generale, i focus qui sotto scendono nel dettaglio per mostrarci **quali specifici valori** spingono verso il ritardo o verso la sicurezza. La logica visiva è identica: la scatola colorata racchiude il cuore dei progetti (il 50% centrale della distribuzione), mentre la linea rossa fissa la soglia di rischio zero.

## Il peso della geografia {#dip-territorio}

{% include altair.html id="vis-territorio" file="/assets/charts/vis_territorio.json" %}

Il territorio non ammette sfumature e mostra **due distribuzioni nettamente separate**. I progetti del Mezzogiorno (color oro) si collocano abbondantemente a destra, confermandosi il bacino di rischio principale. Quelli del Centro-Nord (in viola) si posizionano tutti a sinistra, nell'area di sicurezza. È la stessa spaccatura individuata dalla regressione: due modelli matematicamente opposti confermano l'esatta, identica tendenza.

## Il vincolo dei fondi europei {#dip-quota-ue}

{% include altair.html id="vis-quota-ue" file="/assets/charts/vis_quota_ue.json" %}

Nel paragrafo precedente abbiamo visto come i decimali della quota europea vengano usati dal modello per riconoscere i singoli bandi. Ma se sintetizziamo i risultati raggruppando i progetti in base alla sola presenza o assenza di fondi UE, emerge una dinamica strutturale chiara: disporre di fondi europei (in verde) tende a spingere la distribuzione verso l'area di sicurezza, sotto lo zero. Come già rilevato dalla regressione logistica, le scadenze vincolanti e le rigide regole di disimpegno europee agiscono da forte disincentivo ai ritardi, a prescindere dall'importo esatto.

## Cosa si fa con i soldi: la natura dell'intervento {#dip-natura}

{% include altair.html id="vis-natura" file="/assets/charts/vis_natura.json" %}

È il segnale più inequivocabile. L'**acquisto di beni** è l'unica operazione che il modello considera sistematicamente sicura (tutta la distribuzione è sotto lo zero). All'estremo opposto, **erogare contributi ad altri soggetti** o realizzare **lavori pubblici** spinge drammaticamente verso l'alto l'allarme rischio. Ancora una volta, la sequenza di pericolosità è identica a quella stimata dalla regressione.

## Di cosa si parla: il tema {#dip-tema}

{% include altair.html id="vis-tema" file="/assets/charts/vis_tema.json" %}

Anche qui l'identikit regge. Spingono verso l'area di rischio i progetti legati alla **competitività delle imprese**, all'**istruzione** e all'**occupazione**. Agiscono invece da scudo l'**ambiente**, l'**energia** e le **reti digitali**. Rispetto alla regressione, qui notiamo un dettaglio in più: l'estensione orizzontale per ogni tema è molto ampia e attraversa quasi sempre lo zero. Significa che il tema, da solo, non è una condanna automatica, ma interagisce fortemente con il resto del progetto.

## Quanto si spende: la dimensione {#dip-dimensione}

{% include altair.html id="vis-dimensione" file="/assets/charts/vis_dimensione.json" %}

I progetti più piccoli (da 100 a 500 mila euro) sono l'unico gruppo prevalentemente al riparo. Salendo con i fondi, il rischio cresce fino a toccare il suo apice per i progetti **medio-grandi (tra 1 e 10 milioni di euro)**, per poi ridiscendere leggermente sui mega-progetti. È l'esatta forma "a campana" che avevamo già osservato esplorando i dati base.

# Che cosa ci dice, in conclusione

**Costruire un sistema di allerta è possibile.** Utilizzando unicamente i dati noti al momento della firma di un progetto, è possibile ottenere una previsione solida. Non serve a condannare un progetto in partenza, ma a definire liste di priorità su cui attivare controlli preventivi.

**Il punto di forza: catturare le combinazioni complesse.** A differenza della regressione, il Random Forest non valuta i fattori in modo isolato: riesce a cogliere da solo le interazioni a coppie o di gruppo (ad esempio come il rischio di un certo tipo di intervento cambi radicalmente a seconda del territorio in cui si localizza). I valori SHAP ci permettono di "aprire la scatola nera" e verificare che queste combinazioni abbiano un senso logico.

**Due strumenti per due scopi diversi.** Quando le due metodologie concordano sui fattori principali (Mezzogiorno, contributi a soggetti terzi, fasce dimensionali medio-grandi), il dato diventa inoppugnabile. Tuttavia, la scelta dello strumento dipende dall'obiettivo: se l'obiettivo è **anticipare il rischio** sfruttando tutte le interazioni tra le variabili, lo strumento ideale è il **Random Forest**; se l'obiettivo della politica pubblica è **isolare l'effetto netto** di una singola leva normativa a parità di tutto il resto, il riferimento per la quantificazione resta l'Odds Ratio della **regressione**.

