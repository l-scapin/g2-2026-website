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


# Risultati

L'analisi ha individuato tre differenti profili di progetto.

| **Cluster** | **Numero di progetti** |
|:-----------:|-----------------------:|
| 0 | **94.496** |
| 1 | **79.013** |
| 2 | **33.268** ||

Si osserva che:
 
- **Cluster 0** è il più numeroso (circa il 46% dei progetti);
- **Cluster 1** raccoglie circa il 38% dei progetti;
- **Cluster 2** è il più piccolo (circa il 16%).

La distribuzione è abbastanza equilibrata: non esiste un cluster che contenga quasi tutti i progetti o, al contrario, un gruppo estremamente piccolo. 

| | **0** · Servizi e formazione con fondi UE | **1** · Opere e sviluppo con fondi nazionali | **2** · Innovazione con capitale privato |
|---|---|---|---|
| finanziamento pubblico medio | 255.365 € | **570.421 €** | 326.372 € |
| quota di fondi UE | **62,1%** | 8,3% | 45,4% |
| finanziamento privato medio | 0 € | 0 € | **232.529 €** |
| enti coinvolti | **2,31** | 2,03 | 2,12 |

Come si evince, **il Cluster 0** presenta:

- quota di finanziamento europeo molto elevata (62%);
- finanziamento pubblico medio;
- finanziamento privato praticamente assente;
- numero medio più alto di enti coinvolti (2,3).

Questo identifica progetti fortemente sostenuti da fondi europei e leggermente più complessi dal punto di vista della governance.

Il **Cluster 1** si distingue invece per:
- finanziamento pubblico più elevato;
- quota UE molto bassa (8%);
- contributo privato praticamente nullo;
- mediamente poco più di due enti coinvolti.

È quindi il gruppo dei progetti principalmente finanziati da risorse nazionali.

Infine si puo dire che il **Cluster 2** sia quello più particolare, in quanto possiede un'importante componente di finanziamento privato a differenza degli altri gruppi, ma
- mantiene una quota UE intermedia (45%);
- il numero medio di enti è simile a quello degli altri gruppi.

## Confronto con le altre variabili 

Dopo aver confrontato i gruppi con variabili non utilizzate durante il clustering (rischio, macroarea, ciclo di programmazione e tema sintetico), emerge un quadro molto più ricco.

| | **0** · Progetti sociali finanziati dall'UE | **1** · Progetti infrastrutturali e di sviluppo territoriale | **2** · Progetti di innovazione con capitale privato |
|---|---|---|---|
| **progetti a rischio** | **29,0%** | **37,3%** | **31,9%** |
| macroarea prevalente | Mezzogiorno (53,4%) | Mezzogiorno (57,2%) | Mezzogiorno (55,8%) |
| ciclo prevalente | 2007–2013 e 2014–2020 | Distribuito tra tutti i cicli, con maggiore presenza nel 2021–2027 | **2014–2020 (56,3%)** |
| tema prevalente | **Istruzione e formazione** (29,5%)<br>Occupazione e lavoro (20,1%) | Ambiente (18,1%)<br>Inclusione sociale (15,8%)<br>Competitività delle imprese (13,2%) | **Ricerca e innovazione** (42,5%)<br>Competitività delle imprese (37,5%) |
| profilo | Progetti sostenuti prevalentemente da fondi UE, orientati ai servizi sociali e formativi | Progetti di maggiore dimensione economica, finanziati soprattutto da risorse nazionali | Progetti con forte partecipazione privata, focalizzati su innovazione e competitività |


L'analisi a posteriori conferma che i tre cluster non rappresentano soltanto differenze nella struttura finanziaria dei progetti, ma identificano anche profili progettuali distinti.

Il **Cluster 0** raccoglie prevalentemente interventi finanziati dall'Unione Europea, orientati ai temi dell'istruzione, della formazione e dell'occupazione. È inoltre il gruppo che presenta la minore percentuale di progetti classificati come a rischio, suggerendo una maggiore stabilità nella realizzazione.

Il **Cluster 1** è invece caratterizzato da progetti di dimensioni economiche maggiori, finanziati soprattutto da risorse nazionali. È il cluster con la più alta incidenza di progetti a rischio e comprende una maggiore varietà di temi, tra cui ambiente, inclusione sociale, competitività e trasporti.

Il **Cluster 2** si distingue per la presenza di una componente significativa di finanziamento privato. I progetti appartenenti a questo gruppo sono concentrati soprattutto sul ciclo di programmazione 2014–2020 e riguardano prevalentemente ricerca, innovazione e competitività delle imprese, presentando un livello di rischio intermedio.

Infine, il confronto con la macroarea geografica mostra che tutti e tre i cluster sono distribuiti in modo molto simile tra Mezzogiorno e Centro-Nord. Questo suggerisce che la segmentazione individuata da K-Means dipende principalmente dalle caratteristiche economiche e organizzative dei progetti, piuttosto che dalla loro localizzazione geografica. 




# Visualizzazione dei cluster tramite PCA 

Per facilitare l'interpretazione dei risultati, è stata applicata la **Principal Component Analysis (PCA)**, una tecnica di riduzione della dimensionalità che proietta i dati in uno spazio bidimensionale preservando il più possibile la variabilità originale.
La rappresentazione ottenuta mostra che i tre cluster individuati da K-Means occupano regioni differenti dello spazio delle componenti principali. Sebbene sia presente una parziale sovrapposizione tra alcuni punti, i gruppi risultano complessivamente distinguibili.

![Proiezione PCA dei tre gruppi]({{ site.baseurl }}/assets/images/clustering/clu_pca.png){: .img-fluid }

# Conclusioni

L'analisi di clustering ha dunque permesso di individuare tre profili ricorrenti di progetti finanziati attraverso le politiche di coesione:

- progetti sociali e formativi finanziati prevalentemente dall'Unione Europea;
- grandi investimenti pubblici a prevalente finanziamento nazionale;
- progetti di ricerca e innovazione caratterizzati dalla presenza di capitale privato.

Questa segmentazione offre una rappresentazione sintetica della struttura del dataset e costituisce una base utile per le successive analisi predittive. In particolare, evidenzia come differenti configurazioni di finanziamento e governance siano associate a priorità tematiche e livelli di rischio differenti, fornendo una chiave di lettura più approfondita dell'ecosistema dei progetti di coesione.






<hr>

<p style="font-size: 0.8rem; color: #888; margin-top: 1.5rem;">
  Immagine di copertina da <a href="https://unsplash.com" target="_blank" rel="noopener">Unsplash</a>.
</p>