---
layout: default
title: "Clustering"
show_sidetoc: true
header_type: hero #base, post, hero, image, splash
header_img: assets/images/hero_clustering.jpg
header_img_position: center
header_title: "Clustering"
subtitle: "Capire i progetti prima di prevederne il rischio"
---

<!-- Numeri dal notebook di clustering (K-Means, k=3), rieseguito sul parquet slim corrente
     (206.777 x 52, data di riferimento 31/12/2025). Le figure escono da
     01_analisi/figure/make_clustering_sito.py: se il clustering cambia, rilanciare lo script.
     Regole editoriali: mai "causale", "persistente" e NON "strutturale", niente virgolettati
     inventati, nessun risultato pre-affermato. -->

<div class="full-width-wrapper">
    <img src="{{ site.baseurl }}/assets/images/header.svg" alt="sbd-pattern" class="full-width-image">
</div>

L'analisi di **clustering** è stata utilizzata per individuare gruppi omogenei di progetti finanziati attraverso le politiche di coesione, con l'obiettivo di comprendere se esistessero **profili ricorrenti** già osservabili al momento dell'avvio del progetto.
Il clustering rappresenta una tecnica di apprendimento **non supervisionato**: non utilizza una variabile target, ma cerca di raggruppare i progetti che presentano caratteristiche simili.
L'idea è quella di ottenere una segmentazione del dataset utile sia per comprenderne la struttura sia come supporto alle successive analisi predittive.


# Preparazione dei dati 

Per evitare di introdurre informazioni disponibili solo nelle fasi avanzate del progetto, sono state considerate esclusivamente variabili osservabili all'inizio del ciclo di vita (“Giorno 0").
Dopo una fase di esplorazione del dataset, sono state selezionate **quattro caratteristiche** ritenute rappresentative delle dimensioni economiche e organizzative dei progetti:


- finanziamento pubblico totale;
- quota di finanziamento europeo;
- finanziamento privato;
- numero di enti coinvolti.

Prima dell'analisi di clustering vera e propria è stata effettuata una fase di **preprocessing** comprendente:
- verifica dell'assenza di valori mancanti;
- analisi delle correlazioni tra le variabili ed eventuale eliminazione di feature ridondanti;
- trasformazione logaritmica delle variabili monetarie fortemente asimmetriche;
- standardizzazione delle variabili tramite StandardScaler.

# Scelta del numero di cluster

Per il clustering è stato utilizzato un algoritmo noto col nome di **K-Means**, che consente di ottenere una segmentazione chiara, interpretabile e adatta a dataset numerici di grandi dimensioni. 

Per individuare il numero di cluster k più appropriato si possono utilizzare due criteri complementari.

![Elbow Method e coefficiente di silhouette al variare di k]({{ site.baseurl }}/assets/images/clustering/clu_scelta_k.png){: .img-fluid }

Il primo è l’**Elbow Method**, che analizza l'andamento dell'inertia, ossia la somma delle distanze quadratiche tra ciascun progetto e il centroide del cluster di appartenenza. All'aumentare del numero di cluster, l'inertia diminuisce progressivamente; tuttavia, oltre un certo valore di k, il miglioramento diventa marginale. Il punto in cui la curva cambia sensibilmente pendenza, formando un **"gomito"** (elbow), rappresenta un buon compromesso tra qualità della partizione e complessità del modello.

Il secondo criterio è il **Silhouette Score**, che misura contemporaneamente la compattezza dei cluster e la loro separazione. Il coefficiente assume valori compresi tra -1 e 1: valori prossimi a 1 indicano cluster ben distinti e osservazioni correttamente assegnate, mentre valori vicini a 0 suggeriscono una forte sovrapposizione tra i gruppi.

L'analisi congiunta dei due metodi ha evidenziato che una soluzione con **tre cluster** rappresenta il miglior compromesso tra qualità della segmentazione, interpretabilità dei risultati e semplicità del modello. Di conseguenza, il clustering finale è stato ottenuto applicando l'algoritmo K-Means con k = 3.


# I tre gruppi 

L'analisi ha individuato tre differenti profili di progetto.

## Cluster 0 – Progetti a prevalente finanziamento europeo

Questo gruppo comprende circa il 46% dei progetti.
È caratterizzato da:
- finanziamento pubblico relativamente contenuto;
- elevata quota di finanziamento europeo (circa 62%);
- finanziamento privato quasi assente;
- numero leggermente superiore di enti coinvolti.

Dal punto di vista tematico, il cluster è composto prevalentemente da progetti relativi a istruzione e formazione, inclusione sociale e occupazione.
Inoltre presenta la percentuale più bassa di progetti classificati come "a rischio".


## Cluster 1 – Grandi investimenti pubblici nazionali

Questo cluster rappresenta circa il 38% dei progetti.
Le principali caratteristiche sono:
- finanziamento pubblico medio più elevato;
- quota europea molto ridotta (circa 8%);
- assenza quasi totale di capitale privato.
I progetti appartenenti a questo gruppo riguardano più frequentemente interventi ambientali, infrastrutturali e di trasporto.
Tra i tre cluster, questo è quello che mostra la maggiore incidenza di progetti a rischio, suggerendo che gli interventi di maggiore dimensione possano essere più esposti a ritardi o criticità nella realizzazione.

## Cluster 2 – Progetti con partecipazione privata

L’ultimo cluster raccoglie circa il 16% dei progetti.
La caratteristica distintiva è la presenza di un'importante componente di finanziamento privato, accompagnata da livelli intermedi di finanziamento pubblico e di quota europea.
Dal punto di vista tematico, il cluster è fortemente orientato verso:
* ricerca e innovazione;
* competitività delle imprese.
La maggior parte dei progetti appartiene inoltre al ciclo di programmazione 2014–2020.

## Tabella di riepilogo

| | **0** · Servizi con fondi UE | **1** · Opere con fondi nazionali | **2** · Incentivi con capitale privato |
|---|---|---|---|
| progetti | 94.496 (45,7%) | 79.013 (38,2%) | 33.268 (16,1%) |
| finanziamento pubblico medio | 255.365 € | **570.421 €** | 326.372 € |
| quota di fondi UE | **62,1%** | 8,3% | 45,4% |
| capitale privato medio | 0 € | 0 € | **232.529 €** |
| enti coinvolti | 2,31 | 2,03 | 2,12 |
| fondi pubblici gestiti | 45,5 mld (14,4%) | **243,0 mld (77,1%)** | 26,8 mld (8,5%) |
| **progetti a rischio** | **29,0%** | **37,3%** | **31,9%** |



## Analisi dei cluster 

Per comprendere meglio la natura dei gruppi individuati, i cluster sono stati confrontati con alcune variabili non utilizzate durante l'addestramento del modello.
L'analisi ha evidenziato che:
- la distribuzione geografica è piuttosto simile tra i cluster, con una prevalenza di progetti localizzati nel Mezzogiorno e nel Centro-Nord;
- emergono invece differenze significative rispetto al ciclo di programmazione, al tema di intervento e alla percentuale di progetti classificati come a rischio.
Questi risultati suggeriscono che i cluster identificano differenti modelli di finanziamento e di organizzazione dei progetti, più che semplici differenze territoriali.

![Percentuale di progetti a rischio nei tre gruppi, scomposta nelle due componenti]({{ site.baseurl }}/assets/images/clustering/clu_rischio.png){: .img-fluid }



# Visualizzazione dei cluster tramite PCA 

Per facilitare l'interpretazione dei risultati, è stata applicata la Principal Component Analysis (PCA), una tecnica di riduzione della dimensionalità che proietta i dati in uno spazio bidimensionale preservando il più possibile la variabilità originale.
La rappresentazione ottenuta mostra che i tre cluster individuati da K-Means occupano regioni differenti dello spazio delle componenti principali. Sebbene sia presente una parziale sovrapposizione tra alcuni punti, i gruppi risultano complessivamente distinguibili, confermando la bontà della segmentazione ottenuta.



![Proiezione PCA dei tre gruppi]({{ site.baseurl }}/assets/images/clustering/clu_pca.png){: .img-fluid }


# Conclusioni 
L'analisi di clustering ha permesso di individuare tre profili ricorrenti di progetti finanziati attraverso le politiche di coesione:
-progetti sociali e formativi finanziati prevalentemente dall'Unione Europea;
-grandi investimenti pubblici a prevalente finanziamento nazionale;
-progetti di ricerca e innovazione caratterizzati dalla presenza di capitale privato.
Questa segmentazione offre una rappresentazione sintetica della struttura del dataset e costituisce una base utile per le successive analisi predittive. In particolare, evidenzia come differenti configurazioni di finanziamento e governance siano associate a priorità tematiche e livelli di rischio differenti, fornendo una chiave di lettura più approfondita dell'ecosistema dei progetti di coesione.




<hr>

<p style="font-size: 0.8rem; color: #888; margin-top: 1.5rem;">
  Immagine di copertina da <a href="https://unsplash.com" target="_blank" rel="noopener">Unsplash</a>.
</p>