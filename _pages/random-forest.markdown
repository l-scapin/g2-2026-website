---
layout: default
title: "Random Forest"
show_sidetoc: true
vega: true
header_type: hero #base, post, hero, image, splash
header_img: assets/images/hero_random_forest.jpg
header_img_position: center
header_title: "Random Forest"
subtitle: "Quanto lontano si può arrivare a prevedere il rischio"
---

<!-- Numeri dal notebook 04 (Random Forest + SHAP), verificati rieseguendo il modello.
     Regole editoriali: mai "causale", "persistente" e NON "strutturale", niente virgolettati
     inventati, nessun risultato pre-affermato. -->

<div class="full-width-wrapper">
    <img src="{{ site.baseurl }}/assets/images/header.svg" alt="sbd-pattern" class="full-width-image">
</div>

La [regressione]({{ site.baseurl }}/regressione.html) ha risposto alla domanda «**quanto pesa
ciascun fattore**, a parità degli altri». Ne resta una diversa e altrettanto concreta: **quanto
lontano si può arrivare a prevedere** quali progetti si inceppano, prima che accada? Qui la
affrontiamo con un **Random Forest**, un insieme di centinaia di alberi decisionali che cercano da
soli le combinazioni di caratteristiche associate al rischio. La risposta breve: si prevede molto
meglio, ma una parte del guadagno arriva da dove non ce lo aspettavamo.
{: .lead }

# Perché due modelli e non uno {#due-modelli}

Non è una gara fra algoritmi: i due modelli rispondono a domande diverse.

La **regressione logistica** *spiega*. Ogni fattore ha un coefficiente che diventa un odds ratio
con il suo intervallo di confidenza: «al Sud le odds di rischio sono 2,80 volte, fra 2,74 e 2,86».
È il modello che permette di dire *quanto* pesa il territorio a parità di tutto il resto. Il prezzo
è una forma imposta: gli effetti sono additivi, e le eccezioni entrano solo se qualcuno le
specifica a mano.

Il **Random Forest** *prevede*. Costruisce molti alberi su sottoinsiemi diversi dei dati e li fa
votare: così coglie da solo soglie, curve e combinazioni, senza che nessuno gliele suggerisca. Il
prezzo è che non produce coefficienti né intervalli di confidenza: non risponde a «quanto pesa il
territorio», risponde a «chi è a rischio».

Perché il confronto sia leale, il Random Forest riceve **le stesse variabili** della regressione
(territorio, tipo di intervento, tema, dimensione, quota di fondi europei, quota di capitale
privato, numero di enti) ed è valutato **sugli stessi progetti tenuti fuori dall'addestramento**:
70% per imparare, 30% mai visto per giudicare. Gli iperparametri sono scelti con una ricerca
automatica in cross-validation sul solo train.

# Il risultato: si prevede molto meglio {#risultato}

Sul test set il Random Forest ottiene **AUC 0,813**, contro lo **0,669** della regressione
logistica sulle stesse variabili e sullo stesso split. È un salto molto ampio: significa che nel
rischio ci sono soglie e combinazioni che un modello additivo non riesce a catturare.

Il modello non sta imparando a memoria: nella cross-validation l'accuratezza sul training è 0,825
contro 0,805 in validazione, uno scarto piccolo, e il valore sul test set mai visto lo conferma.

![Confronto delle AUC fra logistica e Random Forest]({{ site.baseurl }}/assets/images/modello/rf_confronto_auc.png){: .img-fluid }

## Da dove arriva il guadagno (e perché non va raccontato come una vittoria) {#granularita}

Il grafico qui sopra mostra anche la parte meno comoda, che abbiamo voluto misurare invece di
darla per buona. La variabile più usata dagli alberi è la **quota di fondi europei**, e quella
variabile ha una caratteristica che sfugge a prima vista: assume **oltre 74.000 valori distinti**
su 206.757 progetti, e per la maggior parte di essi il valore è **unico**, appartiene a un solo
progetto. Non si comporta come una percentuale, si comporta come un'impronta digitale.

Quei decimali non sono casuali: identificano il **piano di finanziamento**, e quindi in buona parte
il programma che ha finanziato il progetto, con il suo periodo e la sua amministrazione. Un albero
abbastanza profondo può impararsi che una certa combinazione di decimali corrisponde a un certo
bando, e che quel bando è andato male.

Per quantificarlo abbiamo rifatto il modello arrotondando progressivamente le quote:

| variabili | AUC sul test |
|---|---|
| quote con i valori grezzi | **0,813** |
| quote arrotondate al 10% | 0,778 |
| quote ridotte a un semplice «sì / no» | 0,732 |
| regressione logistica (stesse variabili) | 0,669 |

La lettura onesta è duplice. **Il vantaggio del Random Forest è reale**: anche buttando via tutta
la precisione decimale resta a 0,732, ben sopra la logistica, e quel margine è vero segnale non
lineare. Ma **circa metà del salto dipende dalla capacità di riconoscere il singolo piano di
finanziamento**, cioè un'informazione che assomiglia più a un'etichetta amministrativa che a una
caratteristica del progetto.

Per un sistema di allerta è una buona notizia: quell'informazione esiste il giorno zero ed è lecito
usarla. Per capire *che cosa rende fragile un progetto* è un avvertimento: il modello sta in parte
riconoscendo *da dove viene* il progetto, non *com'è fatto*.

# Che cosa guarda il modello {#shap}

Un modello che segnala progetti senza dire perché è inutilizzabile per chi deve decidere. Per
questo il Random Forest è accompagnato da un'analisi **SHAP**, che scompone ogni singola previsione
nei contributi dei diversi fattori.

{% include altair.html id="vis-importanza-globale" file="/assets/charts/vis_importanza_globale.json" %}

In cima c'è il **territorio**, seguito dalla quota di fondi europei, dal tipo di intervento e dal
tema. Il verdetto della regressione regge anche qui, con un modello che di quel verdetto non sa
nulla e che era libero di dare peso a qualunque cosa.

Merita una nota il fatto che l'indicatore di importanza interno agli alberi darebbe una classifica
diversa, con la quota europea nettamente in testa. La differenza non è un dettaglio tecnico: quella
misura tende a premiare le variabili con moltissimi valori distinti, esattamente il problema
descritto qui sopra, mentre SHAP ne risente molto meno. Le due classifiche a confronto sono un
altro modo di vedere lo stesso fenomeno.

{% include altair.html id="vis-riepilogo-impatto" file="/assets/charts/vis_riepilogo_impatto.json" %}

Questo secondo grafico offre una panoramica sulle **distribuzioni dell'impatto** di tutte le variabili senza la sovrapposizione disordinata di migliaia di punti. La linea tratteggiata rossa segna lo zero: a destra (valori positivi) si trovano i casi in cui la variabile spinge verso il rischio, a sinistra quelli in cui lo riduce. Variabili come il territorio o la quota europea mostrano una forbice molto ampia, capace di spostare la previsione in modo radicale.

# Il dettaglio, fattore per fattore {#dipendenze}

I grafici precedenti dicono *quanto* pesa ciascuna variabile nell'insieme. I boxplot qui sotto scendono nel dettaglio e dicono **quali valori** di quella specifica variabile spingono verso il rischio e quali lo allontanano. Si leggono così: la "scatola" colorata riassume il 50% centrale della distribuzione dei progetti per una determinata categoria; la linea orizzontale rossa fissa lo zero.

## Il territorio {#dip-territorio}

{% include altair.html id="vis-territorio" file="/assets/charts/vis_territorio.json" %}

Il territorio mostra **due distribuzioni nettamente separate**: la mediana dei progetti del Mezzogiorno (in color oro) si colloca abbondantemente a destra, indicando un maggiore rischio, mentre quella del Centro-Nord (in viola) si trova a sinistra.

## Il tipo di intervento {#dip-natura}

{% include altair.html id="vis-natura" file="/assets/charts/vis_natura.json" %}

È il grafico più netto tra le variabili categoriche. L'**acquisto di beni** è l'unica operazione la cui distribuzione si trova quasi interamente sotto lo zero: comprare è l'operazione che il modello considera più sicura. All'estremo opposto i **contributi ad altri soggetti**, seguiti da incentivi e lavori pubblici. I **servizi** stanno a cavallo dello zero, vicini alla media. 
L'ordine è **identico a quello degli odds ratio della regressione**.

## Il tema {#dip-tema}

{% include altair.html id="vis-tema" file="/assets/charts/vis_tema.json" %}

Anche qui la corrispondenza regge. Spingono verso il rischio **competitività delle imprese**, **istruzione e formazione** e **occupazione e lavoro**. Restano intorno allo zero o sotto **ambiente**, **energia**, **cultura** e **reti e servizi digitali**. 
L'estensione dei baffi di ciascun tema è però ampia e attraversa lo zero quasi ovunque: il tema da solo non decide quasi nulla, ma sposta la previsione di poco in entrambe le direzioni a seconda dell'interazione con il resto del progetto.

## La dimensione {#dip-dimensione}

{% include altair.html id="vis-dimensione" file="/assets/charts/vis_dimensione.json" %}

I progetti più piccoli (100k-500k) sono l'unico gruppo prevalentemente sotto lo zero: la taglia minima protegge. Salendo di dimensione la mediana diventa positiva e raggiunge il massimo nelle fasce centrali, fra 1 e 10 milioni, creando la stessa **campana** trovata dalla regressione. La fascia oltre i 50 milioni ha pochissimi elementi nell'archivio (appena 623), motivo per cui l'estensione statistica risulta più contratta.

# Che cosa ci dice, in conclusione

**Prevedere si può, e meglio di quanto pensassimo.** Con le sole caratteristiche note alla nascita di un progetto si arriva a un'accuratezza discreta, sufficiente a costruire una lista di sorveglianza: non a dire «questo progetto fallirà», ma a dire «questi meritano un controllo prima degli altri».

**Il verdetto sul territorio non cambia.** Due modelli con logiche opposte, uno che impone una forma e uno che la cerca da solo, mettono il Mezzogiorno in cima alla lista dei fattori. È la conferma incrociata più solida che potessimo avere.

**Ma prevedere non è spiegare.** Il Random Forest vince sulla previsione e resta muto sul perché, mentre la regressione dice di quanto pesa ciascun fattore e sa dichiarare la propria incertezza. Per il racconto pubblico e per qualunque proposta di intervento, il numero da citare resta quello della [regressione]({{ site.baseurl }}/regressione.html); il Random Forest serve a stabilire fin dove ci si può spingere, e a ricordare che una parte di ciò che sembra previsione è, in realtà, riconoscere l'amministrazione che ha aperto il bando.