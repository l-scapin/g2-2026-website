---
layout: default
title: "Clustering"
show_sidetoc: true
header_type: hero #base, post, hero, image, splash
header_img: assets/images/hero_clustering.jpg
header_img_position: center
header_title: "Clustering"
subtitle: "Tre famiglie di progetti, trovate senza guardare il risultato"
---

<!-- Numeri dal notebook di clustering (K-Means, k=3), rieseguito sul parquet slim corrente
     (206.777 x 52, data di riferimento 31/12/2025). Le figure escono da
     01_analisi/figure/make_clustering_sito.py: se il clustering cambia, rilanciare lo script.
     Regole editoriali: mai "causale", "persistente" e NON "strutturale", niente virgolettati
     inventati, nessun risultato pre-affermato. -->

<div class="full-width-wrapper">
    <img src="{{ site.baseurl }}/assets/images/header.svg" alt="sbd-pattern" class="full-width-image">
</div>

Fin qui abbiamo chiesto ai dati di rispondere a domande nostre: quanto pesa il territorio, chi si
inceppa di più. Qui facciamo il contrario. Diamo all'algoritmo le sole caratteristiche note il
giorno in cui un progetto nasce, **senza dirgli nulla sul rischio**, e gli chiediamo di raggruppare
da solo i 206.777 progetti. Se i gruppi che trova avessero tassi di rischio diversi, sarebbe una
conferma che arriva da un metodo che non sapeva cosa stesse cercando.
{: .lead }

# Le quattro variabili del giorno zero {#feature}

Il clustering riceve **quattro variabili**, le stesse selezionate in fondo
all'[analisi esplorativa]({{ site.baseurl }}/eda.html#correlazioni): l'**importo** del
finanziamento pubblico, la **quota di fondi europei**, il **capitale privato** e il **numero di
enti coinvolti**. La regola che le ha scelte è una sola: devono essere note **al momento
dell'approvazione**, prima che il progetto cominci.

È un vincolo che esclude di proposito le variabili più tentanti. Il **tasso di assorbimento**, per
esempio, separerebbe benissimo i progetti, ma è quasi un esito: raggrupparli in base a quanto hanno
speso e poi scoprire che i gruppi hanno rischi diversi vorrebbe dire ritrovare quello che ci si è
messo dentro. Fuori anche pagamenti, ritardi e date effettive, per la stessa ragione.

Due dettagli tecnici, entrambi con una conseguenza sulla lettura. Le due grandezze in euro entrano
in **logaritmo**, perché gli importi sono molto asimmetrici e senza la trasformazione una manciata
di progetti da centinaia di milioni deciderebbe da sola i gruppi. E il capitale privato entra in
**valore assoluto**, non come quota sul totale: è la scelta fatta nel notebook, e conta, perché
vale zero per l'84% dei progetti. Su questo torniamo alla fine, quando si tratta di dire cosa
regge e cosa no.

Le quattro variabili sono **poco correlate fra loro** (fuori dalla diagonale il coefficiente più
alto è 0,20), quindi nessuna delle quattro sta contando due volte la stessa cosa. Prima di
raggrupparle vengono **standardizzate**: K-Means ragiona per distanze, e senza standardizzare la
variabile con i numeri più grandi deciderebbe tutto.

# Quanti gruppi? {#scelta-k}

Il metodo è **K-Means**: si fissa il numero di gruppi, l'algoritmo cerca le posizioni che rendono i
gruppi più compatti possibile. Il numero non lo sceglie lui, e i due criteri abituali qui non
vanno d'accordo.

![Curva dell'inerzia e coefficiente di silhouette al variare di k]({{ site.baseurl }}/assets/images/clustering/clu_scelta_k.png){: .img-fluid }

Il **gomito** (a sinistra) misura quanto sono compatti i gruppi: scende sempre, perché aggiungendo
gruppi la compattezza migliora comunque, e si cerca il punto in cui smette di scendere in fretta.
Qui il rallentamento arriva fra 4 e 5. Il **coefficiente di silhouette** (a destra) misura una cosa
diversa, cioè quanto ogni progetto sta meglio nel proprio gruppo che nel gruppo più vicino: qui un
massimo esiste, ed è su **k = 3** con **0,473**.

Abbiamo tenuto **tre gruppi**, per due ragioni dichiarate: è il valore che massimizza la
separazione secondo il criterio che una risposta la dà, ed è il numero che produce gruppi
raccontabili. Va detto per intero: 0,473 è una separazione **discreta, non netta**. I gruppi si
distinguono, ma non sono tre isole.

# I tre gruppi {#profili}

Ecco che cosa distingue i tre gruppi sulle quattro variabili che li hanno generati.

![Medie delle quattro variabili nei tre gruppi]({{ site.baseurl }}/assets/images/clustering/clu_profili.png){: .img-fluid }

La lettura è netta: i tre gruppi si separano su **come è finanziato** il progetto, non su quanto è
complicato gestirlo. Il numero di enti coinvolti è praticamente lo stesso nei tre (2,31 · 2,03 ·
2,12) e non contribuisce quasi nulla alla divisione.

| | **A** · Servizi con fondi UE | **B** · Opere con fondi nazionali | **C** · Incentivi con capitale privato |
|---|---|---|---|
| progetti | 94.496 (45,7%) | 79.013 (38,2%) | 33.268 (16,1%) |
| finanziamento pubblico medio | 255.365 € | **570.421 €** | 326.372 € |
| quota di fondi UE | **62,1%** | 8,3% | 45,4% |
| capitale privato medio | 0 € | 0 € | **232.529 €** |
| enti coinvolti | 2,31 | 2,03 | 2,12 |
| fondi pubblici gestiti | 45,5 mld (14,4%) | **243,0 mld (77,1%)** | 26,8 mld (8,5%) |
| **progetti a rischio** | **29,0%** | **37,3%** | **31,9%** |

I nomi non escono dall'algoritmo, che vede solo numeri: li abbiamo dati noi guardando che tipo di
progetti sono finiti in ciascun gruppo.

**A · Servizi con fondi UE** è il gruppo più numeroso e il più piccolo per taglia media. Sono per
metà (50,9%) **acquisti o realizzazioni di servizi**, e i temi dominanti sono **istruzione e
formazione** (29,5%) e **occupazione e lavoro** (20,1%): la parte immateriale della coesione,
quella tipicamente finanziata dal Fondo Sociale Europeo, il che spiega la quota UE più alta dei tre.

**B · Opere con fondi nazionali** è il gruppo dei cantieri: **lavori pubblici** al 53,3%, con
ambiente (18,1%) e trasporti (12,1%) fra i temi. Ha l'importo medio più alto e la quota europea più
bassa, cioè è la parte di coesione pagata soprattutto con fondi italiani (FSC e cofinanziamenti).
È anche l'unico gruppo che contiene ancora una quota rilevante del ciclo **2000-2006** (12,2%).
Il dato da tenere: con il 38% dei progetti gestisce **il 77% di tutto il denaro**.

**C · Incentivi con capitale privato** è il gruppo più netto dei tre: **incentivi a unità
produttive** al 77,8%, temi **ricerca e innovazione** (42,5%) e **competitività delle imprese**
(37,5%), e un cofinanziamento privato medio di 232.529 €. È molto concentrato nel ciclo
**2014-2020** (56,3%) e quasi assente nel 2021-2027 (1,1%).

## Il territorio non c'entra {#territorio}

Un controllo che valeva la pena fare, visto che il divario Nord-Sud è il filo di tutto il progetto:
i tre gruppi **non** sono tre geografie. Fra i progetti localizzati in una delle due macroaree, la
quota di Mezzogiorno è **54,5%** nel gruppo A, **57,6%** nel B e **56,2%** nel C, contro il 56,0%
del totale. Uno scarto di poco più di un punto in ciascuna direzione.

Serve a interpretare bene la riga più importante della tabella: le differenze di rischio fra i tre
gruppi **non sono il divario territoriale travestito**. Sono differenze fra tre modi di finanziare
un progetto, misurate su gruppi che contengono Nord e Sud nelle stesse proporzioni.

# Il rischio dei tre gruppi {#rischio}

Qui entra in scena la variabile che il clustering **non** ha mai visto.

![Percentuale di progetti a rischio nei tre gruppi, scomposta nelle due componenti]({{ site.baseurl }}/assets/images/clustering/clu_rischio.png){: .img-fluid }

I tre tassi sono **29,0% · 37,3% · 31,9%**, contro una media generale del 32,6%. Lo scarto fra il
gruppo migliore e il peggiore è di **otto punti**, e va nella direzione già vista altrove: il gruppo
dei **lavori pubblici a finanziamento nazionale** è quello che si inceppa di più, ed è anche quello
che muove tre quarti dei soldi. Tenuto conto che l'algoritmo non sapeva nulla del rischio, il fatto
che i gruppi si dispongano in ordine è già un risultato.

Ma il numero interessante è nella **scomposizione**, non nel totale. Le due componenti del rischio,
i progetti mai partiti e quelli partiti e fuori tempo massimo, si comportano in modo opposto nei tre
gruppi:

- **B** ha la quota più alta di progetti **mai avviati**, **11,1%** contro il 7,9% della media
  generale: fondi assegnati a opere che non hanno ancora aperto il cantiere;
- **C** ha la quota più bassa in assoluto, **2,3%**, cioè poco più di due progetti su cento. Dove
  c'è un privato che cofinanzia il proprio investimento, il progetto quasi sempre parte;
- **ma proprio C** ha la quota più alta di progetti **fuori tempo massimo** (29,6%, contro 26,2 di
  B e 21,9 di A).

Vale la pena fermarsi sulla terza riga, perché smonta una lettura comoda. Un gruppo che parte quasi
sempre e poi sfora è un gruppo che ha un problema di **esecuzione**, non di avvio. E soprattutto, il
capitale privato qui **non** è un fattore protettivo: i progetti che ne hanno partono di più e
chiudono in ritardo di più. La differenza è quasi certamente di **selezione**, non di trattamento:
un'impresa che mette soldi propri presenta il progetto quando è pronta a farlo partire, ma il
capitale privato non le accorcia i tempi di realizzazione. È la stessa cautela che accompagna il
coefficiente del capitale privato nella [regressione]({{ site.baseurl }}/regressione.html).

# I gruppi visti in due dimensioni {#pca}

K-Means lavora in quattro dimensioni, che non si disegnano. Per vederli si proietta tutto su un
piano con la **PCA**, cioè si cercano le due combinazioni di variabili che conservano più
variabilità possibile.

![Proiezione PCA dei tre gruppi]({{ site.baseurl }}/assets/images/clustering/clu_pca.png){: .img-fluid }

Ogni pannello accende un gruppo solo sullo sfondo grigio degli altri due: con 206.777 punti
sovrapposti, un unico grafico tricolore direbbe soprattutto quale colore è stato disegnato per
ultimo. I tre gruppi occupano zone riconoscibili e distinte, ma si **toccano**, e nella parte
centrale si sovrappongono.

Due avvertenze per leggerla senza illudersi. Le due componenti conservano il **57%** della
variabilità: quella nell'immagine è una proiezione, non i gruppi per intero, e due punti vicini
sullo schermo possono essere lontani nello spazio vero. E le strisce diagonali visibili nel disegno
non sono un pattern nascosto: sono l'effetto del **numero di enti**, che assume pochi valori interi,
e delle due variabili logaritmiche.

# Che cosa aggiunge questa analisi, e che cosa no {#limiti}

**Quello che aggiunge.** Una conferma che non viene dai modelli: raggruppando i progetti sulle sole
condizioni di partenza, senza nessuna informazione sull'esito, i gruppi che emergono hanno tassi di
rischio diversi e ordinati. La segmentazione dice anche **dove sta il denaro**, e la risposta è
concentrata: un gruppo solo, quello delle opere a finanziamento nazionale, tiene il 77% dei fondi
e ha il rischio più alto. Infine, la scomposizione mostra che i tre gruppi non falliscono nello
stesso modo: B non parte, C parte e non chiude.

**Il limite principale, dichiarato.** Il gruppo C coincide quasi esattamente con «il progetto ha
del capitale privato»: dei 33.400 progetti con capitale privato, **33.268 stanno in C**, e in C non
c'è nient'altro. Poiché quella variabile vale zero per l'84% dei progetti, l'algoritmo l'ha usata
di fatto come un interruttore acceso/spento, e uno dei tre gruppi è nato da lì. Non è un errore, ma
va saputo: il terzo gruppo è meno una scoperta e più una divisione che era già nei dati. Sarebbe
diverso usando la **quota** di capitale privato sul totale, come fanno regressione e Random Forest.

**Le altre cautele.** La silhouette di 0,473 dice separazione discreta e non netta, e il criterio
del gomito indicava 4 o 5 gruppi: la scelta di tre è un compromesso fra qualità della separazione e
leggibilità, non un ottimo indiscutibile. K-Means, inoltre, cerca gruppi di forma sferica e di
dimensione simile, il che è un'ipotesi, non un dato. E i tassi di rischio qui sono **descrittivi**:
dicono che i tre gruppi differiscono, non quanto pesi ciascuna variabile a parità delle altre. Per
quello serve la [regressione]({{ site.baseurl }}/regressione.html).

<hr>

<p style="font-size: 0.8rem; color: #888; margin-top: 1.5rem;">
  Immagine di copertina da <a href="https://unsplash.com" target="_blank" rel="noopener">Unsplash</a>.
</p>
