---
layout: default
title: "Random Forest"
show_sidetoc: true
header_type: hero #base, post, hero, image, splash
header_img: assets/images/header.svg
header_title: "Random Forest"
subtitle: "Quanto lontano si può arrivare a prevedere il rischio"
---

<!-- PAGINA IN PREPARAZIONE: il notebook 03 (Random Forest + SHAP) non è ancora stato eseguito.
     Qui c'è il metodo e il criterio di lettura, scritti PRIMA di vedere i risultati: è una
     garanzia contro il racconto costruito a posteriori. La sezione "I risultati" va riempita
     quando il notebook è pronto, ed è formulata in modo da reggere qualunque esito.
     Regole editoriali: mai "causale", "persistente" e NON "strutturale", niente virgolettati
     inventati, nessun risultato pre-affermato. -->

La [regressione]({{ site.baseurl }}/regressione.html) ha risposto alla domanda «**quanto pesa
ciascun fattore**, a parità degli altri». Ne resta una diversa, e altrettanto concreta: **quanto
lontano si può arrivare a prevedere** quali progetti si inceppano, prima che accada? Per
rispondere serve un modello di natura diversa: un **Random Forest**, cioè un insieme di alberi
decisionali che cerca da solo le combinazioni di caratteristiche associate al rischio.
{: .lead }

<div class="def-box" markdown="1">
**Analisi in corso.** Questa pagina descrive il metodo e il criterio con cui leggeremo i
risultati. I numeri arriveranno alla chiusura dell'analisi.
</div>

# Perché due modelli e non uno {#due-modelli}

Non è una gara fra algoritmi: i due modelli rispondono a domande diverse, e nessuno dei due può
sostituire l'altro.

La **regressione logistica** *spiega*. Ogni fattore ha un coefficiente che diventa un odds ratio
con il suo intervallo di confidenza: «al Sud le odds di rischio sono 2,80 volte, fra 2,74 e
2,86». È il modello che permette di dire *quanto* pesa il territorio a parità di tutto il resto.
Il prezzo è una forma imposta: gli effetti sono additivi, e le eccezioni (una curva, una
combinazione particolare di fattori) entrano nel modello solo se qualcuno le specifica a mano.

Il **Random Forest** *prevede*. Costruisce centinaia di alberi decisionali su sottoinsiemi
diversi dei dati e li fa votare: così coglie da solo le non linearità e le interazioni, senza che
nessuno gliele suggerisca. Il prezzo è che non produce coefficienti né intervalli di confidenza:
non risponde a «quanto pesa il territorio», risponde a «chi è a rischio». È una **scatola nera**,
e va aperta a posteriori.

# Come sarà valutato {#metodo}

Perché il confronto significhi qualcosa, deve essere ad armi pari. Tre vincoli che ci siamo
dati **prima** di eseguire il modello:

- **Stesse variabili.** Il Random Forest riceve la stessa matrice della regressione: territorio,
  tipo di intervento, tema, dimensione, quota di fondi europei, quota di capitale privato, numero
  di enti. Se cambiassero le variabili, il confronto misurerebbe i dati, non gli algoritmi.
- **Valutazione solo su dati mai visti.** Un Random Forest può arrivare a memorizzare i dati su
  cui è addestrato: la sua accuratezza «in casa» non significa nulla. L'unica misura onesta è su
  un insieme di progetti tenuto fuori dall'addestramento.
- **Un numero da battere, dichiarato in anticipo.** La regressione ottiene
  **AUC 0,665** su dati mai visti. È questa la soglia rispetto a cui il Random Forest verrà
  giudicato.

# Aprire la scatola nera: SHAP {#shap}

Un modello che indica progetti a rischio senza spiegare perché è inutilizzabile da chi deve
decidere. Per questo affianchiamo al Random Forest l'analisi **SHAP**, che scompone ogni singola
previsione nei contributi dei diversi fattori: non solo «questo progetto è a rischio», ma «lo è
soprattutto per la sua dimensione e per il tipo di intervento».

Un'avvertenza va messa subito, perché è il malinteso più comune: SHAP spiega **le previsioni del
modello**, non il fenomeno. Se il modello sbaglia, SHAP spiega diligentemente l'errore. Resta
uno strumento di lettura, non una prova.

# Che cosa cercheremo (e come lo leggeremo) {#lettura}

Il risultato interessante non è «il Random Forest vince». Sono due, e sono entrambi informativi:

- **Se il guadagno rispetto alla regressione è ampio**, vuol dire che nel rischio ci sono
  combinazioni e soglie che un modello additivo non cattura: varrà la pena cercarle con SHAP e
  raccontarle. Una candidata è già nota: il **capitale privato** riduce il rischio solo dentro gli
  incentivi alle imprese e per niente altrove (lo mostra la
  [regressione]({{ site.baseurl }}/regressione.html#odds-ratio)). Alla logistica quella
  distinzione va dichiarata a mano; un Random Forest dovrebbe trovarla da solo. Se SHAP la fa
  riemergere è una conferma incrociata, e lo scriviamo avendolo previsto prima.
- **Se il guadagno è modesto**, la conclusione è altrettanto netta, e forse più utile: con le
  sole caratteristiche note alla nascita di un progetto, il segnale disponibile è quello. Per
  prevedere meglio non servirebbero modelli più potenti, ma **dati diversi**: l'avanzamento dei
  pagamenti nel tempo, i passaggi amministrativi, i tempi delle procedure di gara.

Una cautela che vale in entrambi i casi. Le caratteristiche usate devono essere note al **giorno
zero** del progetto: usare informazioni che si accumulano *durante* la vita del progetto (quanto
ha speso, a che punto è) produce numeri brillanti e circolari, perché si sta prevedendo
l'esito con l'esito. Lo stesso criterio vale per le descrizioni testuali dei progetti, che
possono aggiungere segnale ma anche limitarsi a riconoscere il programma di finanziamento, e con
esso il territorio e il periodo, cioè informazioni che il modello già ha.

# I risultati

<div class="def-box" markdown="1">
**[SEZIONE DA COMPLETARE]**: qui andranno l'accuratezza ottenuta su dati mai visti, il confronto
con la soglia della regressione, i fattori che il modello usa di più e la lettura SHAP.
</div>

Qualunque sia l'esito, resterà valido il punto di fondo emerso dalla
[regressione]({{ site.baseurl }}/regressione.html): quanto pesa ciascun fattore *a parità degli
altri* lo dice quel modello, non questo. Il Random Forest aggiunge una risposta diversa, cioè
fin dove si può spingere la previsione, e serve a stabilire un limite, non a riscrivere il verdetto.
