---
layout: default
title: "Text Analysis"
show_sidetoc: true
header_type: hero
header_img: assets/images/hero_text_analysis.jpg
header_img_position: center
header_title: "Il peso delle parole"
subtitle: "Cosa si nasconde nelle descrizioni dei progetti"
---

Il [Random Forest]({{ site.baseurl }}/random-forest.html) ha raggiunto un'affidabilità predittiva molto buona utilizzando esclusivamente dati strutturati (importi, localizzazione, tema, tipologia di progetto...). Ma nel database di OpenCoesione esiste un campo testuale libero, che include una **sintesi del progetto**. 

La domanda a cui questa sezione cerca di rispondere è: c'è un'informazione utile in quelle parole che le tabelle non riescono a catturare? E, soprattutto, il linguaggio utilizzato nella fase di progettazione contribuisce a identificare, già all'avvio, i progetti con maggiori probabilità di incepparsi?
{: .lead }

<div class="def-box" style="margin: 25px 0;">
  <p class="def-box__label">Il verdetto in sintesi</p>
  <h4>Il testo smaschera la burocrazia (e porta un segnale reale)</h4>
  <p>L'integrazione dell'analisi testuale porta un guadagno predittivo modesto (circa +1% di affidabilità), ma estremamente solido. Il vero valore di questa analisi, tuttavia, è diagnostico: ci ha permesso di scoprire che gran parte del "linguaggio" usato nei progetti è in realtà costituito da bandi clonati in serie. Una volta ripulito il dato da questo "burocratese", le parole ci confermano la tendenza già vista nei dati strutturati: gli interventi legati alla ricerca e all'imprenditoria affrontano percorsi molto più accidentati rispetto alla formazione scolastica e alle procedure formali.</p>
</div>

# Il corpus disponibile

Il primo passo consiste nel misurare quanto testo sia effettivamente a nostra disposizione. A differenza dei dati finanziari, la descrizione del progetto è un campo facoltativo. 

Sebbene il dataset OpenCoesione contenga oltre 206 mila progetti, solo **107.988 presentano una descrizione compilata** (circa il 52% del totale). L'analisi mostra inoltre una distribuzione non uniforme tra i diversi cicli di programmazione: i progetti dei cicli 2000-2006 e 2014-2020 sono quasi interamente coperti, mentre quelli più datati (2007-2013) o appena partiti (2021-2027) ne sono quasi privi. Le analisi testuali poggiano quindi su un sottoinsieme specifico, dominato dal ciclo 2014-2020.

<figure class="fig-home">
  <img src="{{ site.baseurl }}/assets/images/ta_copertura_testo.png"
       alt="Grafico a barre sulla copertura del corpus testuale">
  <figcaption>
    La copertura non è uniforme tra i cicli di programmazione: due cicli sono completi, due quasi vuoti.
  </figcaption>
</figure>

# Preprocessing: la normalizzazione del testo

Prima di poter utilizzare le descrizioni nei modelli predittivi, è stato necessario effettuare una rigorosa fase di pulizia per ottenere un *corpus* confrontabile e realmente informativo. Le operazioni hanno incluso:

*   **Lemmatizzazione tramite `spaCy`:** Riduzione delle parole alla loro radice linguistica (es. trasformando "realizzazione" e "realizzato" nel verbo "realizzare") per evitare la frammentazione del vocabolario.
*   **Filtraggio grammaticale:** Eliminazione della punteggiatura e delle *stop word* standard (preposizioni, articoli, congiunzioni).
*   **Stop word di dominio:** Definizione ed eliminazione di una lista di parole specifiche del dominio amministrativo che non aggiungono valore predittivo, divise in burocratese onnipresente (es. `progetto`, `intervento`) e lessico dei finanziamenti (es. `euro`, `FESR`).
*   **Pulizia dei segnaposto:** Eliminazione di circa 5.600 descrizioni costituite esclusivamente da caratteri privi di contenuto informativo (come `....` o `ND`), che rappresentavano testo mancante travestito da testo presente.

# Quanto vale il testo da solo?

Prima di combinare il linguaggio con le variabili strutturali, abbiamo valutato quanto fosse informativo di per sé. 

Per rappresentare le descrizioni abbiamo trasformato il testo in numeri attraverso una matrice **TF-IDF** (*Term Frequency - Inverse Document Frequency*), calcolando non solo le singole parole (unigrammi) ma anche le associazioni di due parole (bigrammi). Questa matrice è stata utilizzata come input per una **Regressione Logistica**. 

Il modello puramente testuale ha raggiunto un'affidabilità (AUC) pari a **0,77**, un risultato sorprendentemente vicino allo **0,80** ottenuto dal Random Forest addestrato, su questo stesso sottoinsieme, con le sole variabili strutturali. La sola descrizione del progetto contiene quindi una quantità significativa di informazioni sul rischio futuro.

# Integrare testo e numeri: un miglioramento da pesare con cura

Per migliorare il modello predittivo principale, occorreva unire le due fonti. Inserire direttamente decine di migliaia di *feature* TF-IDF all'interno del Random Forest ne avrebbe compromesso l'efficienza. 

Abbiamo quindi adottato un approccio più compatto tramite *stacking*: il modello testuale (la regressione logistica) produce un **punteggio di rischio ("text score")**, calcolato con tecnica *out-of-fold* per evitare sovradattamenti. Questo singolo punteggio viene poi aggiunto come nona colonna alle feature strutturali.

L'integrazione di questa sintesi numerica del linguaggio porta l'AUC del Random Forest da 0,80 a **0,83**, con un miglioramento apparente di **+3 punti percentuali**.

# Le verifiche contro il data leakage

Un miglioramento così marcato solleva un dubbio metodologico: il modello sta davvero interpretando il linguaggio, o sta semplicemente riconoscendo i bandi amministrativi attraverso la presenza di descrizioni ripetute (i cosiddetti "bandi fotocopia") o il lessico tipico di un decennio rispetto a un altro?

Per scongiurare l'effetto di *data leakage*, sono stati effettuati due controlli stringenti:
1.  **Split per testo unico:** Lo split dei dati tra fase di addestramento e di test è stato vincolato affinché descrizioni identiche non potessero mai comparire in entrambi i gruppi.
2.  **Isolamento del calendario:** L'analisi è stata ristretta al solo ciclo di programmazione 2014-2020, disinnescando le differenze linguistiche temporali.

In entrambi i casi, l'impatto del testo si riduce fisiologicamente: il "guadagno" predittivo passa dall'iniziale +3 a un modesto ma solido **+1%** (portando l'AUC del ciclo '14-'20 da **0,83** del modello base allo **0,84** del modello integrato). Il contributo del testo si assottiglia, dunque, ma rimane reale e significativo. Questo conferma che le descrizioni contengono informazioni intrinseche utili, e non soltanto anomalie algoritmiche dovute alla ripetizione seriale dei bandi.

# Quali parole caratterizzano i progetti?

Analizzando il contenuto lessicale, è emerso che molte delle parole associate ai tassi di rischio più estremi (sia in positivo che in negativo) non rappresentavano veri concetti progettuali, ma facevano riferimento a specifici bandi, emergenze territoriali o meri refusi di trascrizione di singoli uffici. 

Per restituire un vocabolario rappresentativo, abbiamo imposto un filtro di sbarramento: analizzare solo i termini presenti in **almeno 100 descrizioni del tutto distinte**. 

<figure class="fig-home">
  <img src="{{ site.baseurl }}/assets/images/ta_termini_rischio.png"
       alt="Le parole agli estremi del rischio ripulite dai bandi fotocopia">
  <figcaption>
    L'identikit semantico del rischio dopo aver rimosso i bandi clonati. Un termine associato al rischio non è una "causa" del ritardo, ma il segno che quel determinato intervento storicamente ha incontrato più ostacoli. Grafico realizzato con Altair.
  </figcaption>
</figure>

Per esplorare visivamente queste differenze tematiche, il grafico evidenzia come le parole legate all'istruzione e ai passaggi di rendicontazione (in verde) tendano ad associarsi a percorsi più sicuri e fluidi rispetto a termini che richiamano la complessità del mondo aziendale, dei dipartimenti e della ricerca (in rosso).

### La lunghezza della descrizione conta?

Un'ulteriore analisi esplorativa ha valutato la relazione tra la lunghezza della descrizione e la probabilità di rischio. I risultati mostrano che descrizioni molto brevi non sono necessariamente associate a performance peggiori. Tuttavia, le descrizioni più corpose (oltre le 60 parole) risultano mediamente associate a una minore percentuale di progetti a rischio. L'effetto è presente, ma relativamente contenuto, e da solo non costituisce un indicatore primario.

# Conclusioni: oltre le formule burocratiche

L'immersione nel testo libero dei progetti ci consegna una lezione preziosa, che unisce la statistica alla realtà amministrativa. Inizialmente, abbiamo scoperto che quando un modello predittivo legge le descrizioni della Pubblica Amministrazione, il suo primo istinto non è comprendere il "senso" del progetto, ma sfruttare i testi ripetuti per riconoscere il bando o la scrivania di origine. 

Tuttavia, una volta disinnescata questa illusione statistica, il verdetto è chiaro: **il linguaggio contiene un segnale predittivo reale e misurabile**. Il modesto ma solido guadagno di affidabilità (+1% di AUC) ci dice che il modo in cui un progetto viene raccontato nasconde indizi sul suo destino. E, cosa ancora più importante, le "parole del rischio" confermano in pieno l'identikit tracciato dai modelli strutturali: fare ricerca, coinvolgere dipartimenti o erogare incentivi alle aziende porta con sé una complessità che sfocia più facilmente nel ritardo, rispetto alla regolarità della formazione scolastica o al collaudo formale di procedure già codificate.

Per un decisore pubblico, questo significa due cose. Primo: le variabili strutturali (dove si fa il progetto, quanti soldi muove, di che natura è) restano la bussola più potente per inquadrare il rischio al "giorno zero". Secondo: imporre e curare descrizioni testuali che siano davvero *uniche* e di qualità, abbandonando la prassi dei "bandi fotocopia" e del burocratese di riempimento, potrebbe in futuro fornire ai sistemi di monitoraggio preventivo un'arma ancora più affilata per intercettare le criticità di percorso prima che diventino croniche.