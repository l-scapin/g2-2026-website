---
layout: default
title: "Regressione"
show_sidetoc: true
header_type: hero #base, post, hero, image, splash
header_img: assets/images/hero_regressione.jpg
header_img_position: center 
header_title: "La regressione"
subtitle: "Che cosa pesa davvero sul rischio, a parità di tutto il resto"
---

<!-- Regole editoriali: mai "causale" come claim (dire il contrario va bene), "persistente"
     e NON "strutturale", niente virgolettati inventati, nessun esito pre-affermato.
     I numeri di questa pagina vengono dal notebook 02 (regressione logistica, sm.Logit). -->

<div class="full-width-wrapper">
    <img src="{{ site.baseurl }}/assets/images/header.svg" alt="sbd-pattern" class="full-width-image">
</div>

L'analisi esplorativa lascia aperta la domanda decisiva: il divario Nord-Sud conta *di per sé*,
o riflette soltanto il tipo di progetti che il Sud ospita, più grandi, di temi diversi, con
finanziamenti diversi? Qui rispondiamo con una **regressione logistica** sulla variabile
[«a rischio»]({{ site.baseurl }}/eda.html#metriche): un modello che misura il peso di ogni
fattore **a parità di tutti gli altri**. Il verdetto arriva subito: il territorio pesa, e con
lui pesa una variabile che l'esplorazione non aveva messo a fuoco: **il tipo di intervento**.
{: .lead }

# La domanda e il metodo

Un divario descrittivo, per quanto netto, può sempre essere un **effetto di composizione**: se al
Sud ci fossero più progetti grandi, o più opere pubbliche, il gap potrebbe spiegarsi senza
scomodare il territorio. La regressione serve esattamente a questo: mette tutti i fattori nello
stesso modello e chiede a ciascuno quanto conta *tenendo fermi gli altri*.

Il modello è **esplicativo, non una scatola nera**. È stimato per massima verosimiglianza con
`statsmodels`, che oltre ai coefficienti restituisce errori standard, intervalli di confidenza e
p-value: ogni numero di questa pagina ha quindi la sua misura di incertezza.

# Che cosa entra nel modello {#matrice}

Lavoriamo su **206.757 progetti**, cioè l'intero archivio meno una ventina di casi privi della
classificazione di base. Il target è «a rischio»; i fattori messi a confronto sono:

- **Territorio**: Mezzogiorno contro Centro-Nord, la variabile sotto processo;
- **Tipo di intervento**: lavori pubblici, servizi, incentivi alle imprese, contributi ad altri
  soggetti, acquisto di beni (riferimento: *acquisto di beni*);
- **Tema**: le categorie tematiche di OpenCoesione (riferimento: *ambiente*);
- **Dimensione**: classi di importo (riferimento: *100k–500k €*);
- **Fondi europei**: la quota del finanziamento pubblico coperta dall'Unione;
- **Capitale privato**: la quota del costo totale messa da soggetti privati;
- **Governance**: il numero di enti coinvolti nel progetto.

Ogni fattore categoriale si legge **rispetto alla propria categoria di riferimento**. In tutto 26
parametri su oltre 200.000 progetti: un modello volutamente sobrio, con pochissimo spazio per
l'overfitting, e infatti, come vedremo, non ce n'è.

Due scelte vanno dichiarate. Il **ciclo di programmazione non è tra i fattori**: non è una
caratteristica del progetto, è la finestra temporale in cui lo osserviamo: un progetto del
2021-2027 non è più fragile per natura, ha semplicemente avuto meno tempo. Lo usiamo invece come
**verifica**, ristimando il modello dentro ciascun ciclo separatamente. E i progetti non
attribuibili a un territorio (estero, ambito nazionale) restano nei dati con un indicatore
tecnico che li isola, così da non finire confusi con il Centro-Nord.

# Chi pesa davvero {#odds-ratio}

L'**odds ratio (OR)** dice quanto cambiano le probabilità relative di finire a rischio rispetto
alla categoria di riferimento, tenendo fisso tutto il resto: sopra 1 più rischio, sotto 1 meno.
Il grafico mostra tutti gli OR con il loro intervallo di confidenza al 95%.

![Forest plot degli odds ratio sul rischio]({{ site.baseurl }}/assets/images/modello/mod_forest_rischio.png){: .img-fluid }

**Territorio: OR 2,80** (IC 95% [2,74–2,86]). A parità di tipo di intervento, tema, dimensione,
fonti di finanziamento e governance, per un progetto del Mezzogiorno il rapporto fra la probabilità di
incepparsi e quella di non incepparsi è **quasi il triplo** che al Centro-Nord. Il divario visto
nell'esplorazione non era il riflesso del mix di progetti: aggiungere controlli non lo scioglie.

**Il tipo di intervento, la scoperta del modello.** È il fattore più forte dopo il territorio, e
non era emerso nell'analisi descrittiva. Rispetto a un progetto che si limita a comprare beni:

| Tipo di intervento | Odds ratio |
|---|---|
| Contributi ad altri soggetti | **2,34** |
| Lavori pubblici | **1,81** |
| Incentivi alle imprese | 1,54 |
| Servizi | 1,25 |

Detta semplice: **costruire un'opera, o passare i soldi a qualcun altro perché li spenda, è molto
più rischioso che comprare**. Una parte del rischio non sta in chi realizza il progetto, ma in
che cosa il progetto è.

**Tema.** In testa la **competitività delle imprese** (OR 2,14), poi istruzione e formazione
(1,66) e occupazione (1,56). Energia e reti digitali non si distinguono dall'ambiente: sono i
temi che viaggiano meglio, come già mostrava l'esplorazione.

**Fondi europei: OR 0,78.** Un progetto interamente finanziato dall'Unione ha odds di rischio
inferiori di circa un quinto rispetto a uno interamente nazionale e, specularmente, è più
probabile che si concluda. Una lettura plausibile è che i fondi europei portino con sé scadenze
vincolanti e regole di disimpegno; il dato però dice che i due fenomeni vanno insieme, non che
l'uno produca l'altro. Quel che conta è soprattutto **avere** fondi europei più che la quota
esatta: a parità di averli, una percentuale più alta non protegge di più.

**Capitale privato: OR 0,68, ma solo dove il privato mette i soldi suoi.** Passare da un progetto
interamente pubblico a uno interamente cofinanziato da privati riduce le odds di rischio di circa
un terzo. L'effetto però non è distribuito in modo uniforme, e conviene dirlo subito: si concentra
sugli **incentivi alle imprese**, l'unica categoria in cui il cofinanziamento privato è diffuso
(54% dei casi, contro il 5% di tutto il resto). Dentro quel gruppo chi cofinanzia è a rischio nel
31,8% dei casi contro il 36,6%; fuori, la differenza non è distinguibile da zero. È anche un caso
da manuale di **autoselezione**: un'impresa che mette i propri soldi sceglie progetti che ha
davvero intenzione di realizzare, quindi il modello vede una correlazione, non l'effetto del
cofinanziamento.

**Dimensione.** Il rischio disegna una campana: massimo nelle **fasce intermedie** (5–10 milioni,
OR 1,64), più contenuto agli estremi.

**Governance: OR 0,96.** Più enti coinvolti **non** aumentano il rischio. È la conferma
multivariata di quanto l'esplorazione suggeriva: l'ipotesi «più mani sul progetto, più ritardi»
non regge sui nostri dati.

# Quanto è solido il risultato

Con oltre 200.000 progetti, quasi l'intera popolazione, gli errori standard sono minuscoli e
tutti i p-value sono prossimi a zero. Le verifiche che contano davvero, però, sono altre due.

## E se togliessimo il territorio? {#sensibilita}

L'obiezione ricorrente è che l'effetto dell'area sia scontato, e che tanto valga toglierla dal
modello. L'abbiamo testato stimando lo stesso modello **senza** il territorio. Il risultato è che
il modello distingue molto peggio i progetti a rischio (AUC da **0,668** a **0,610**) e il test
del rapporto di verosimiglianza è enorme: il territorio porta informazione che nessun altro
fattore contiene.

Ma il danno peggiore è un altro, ed è **la distorsione degli altri coefficienti**. Senza il
controllo territoriale l'effetto dei fondi europei quasi sparisce (da 0,78 a 0,96), quello del
capitale privato si attenua (da 0,68 a 0,74) e i progetti sopra i 50 milioni sembrano più fragili
di quanto siano (da 1,24 a 1,48). Progetti giganti, fondi europei e cofinanziamento privato non
sono distribuiti allo stesso modo tra Nord e Sud: senza il territorio in modello sono loro ad
assorbirne l'effetto, e a raccontare una storia gonfiata. Togliere l'area non semplifica il modello: **lo
sbaglia**.

## Il divario, ciclo per ciclo {#per-ciclo}

Il modello stima un unico OR del Mezzogiorno, mediato su progetti di età molto diversa. Per
capire se il divario sia il fenomeno di una stagione particolare, ristimiamo lo stesso modello
**dentro ogni ciclo di programmazione**, uno alla volta.

| Ciclo | OR Mezzogiorno |
|---|---|
| 2000-2006 | **17,3** [14,0–21,4] |
| 2007-2013 | **3,84** [3,68–4,01] |
| 2014-2020 | **3,72** [3,59–3,85] |
| 2021-2027 | **1,42** [1,35–1,49] |

Il divario è **maggiore di 1 e statisticamente significativo in tutti e quattro i cicli**: cambia
l'intensità, mai il segno. Due cautele di lettura: nel 2000-2006, ciclo ormai chiuso, al
Centro-Nord è rimasto a rischio quasi nulla, quindi il rapporto esplode, e infatti l'intervallo
è largo; nel 2021-2027, appena partito, quasi tutto è «non ancora a rischio» ovunque, e il
divario può ancora allargarsi. Da notare che dentro i due cicli centrali, quelli con più progetti
e più storia alle spalle, il divario è **più netto** del 2,80 medio: mediare su cicli diversi lo
attenua.

Il divario è dunque **persistente**: non l'eredità di una stagione sfortunata, ma una costante
di venticinque anni di programmazione.

# Quanto prevede? {#auc}

Oltre a spiegare, il modello può provare a **prevedere** quali progetti finiranno a rischio: un
potenziale sistema di allarme preventivo. La capacità di ordinare correttamente i progetti si
misura con l'**AUC** della curva ROC.

![Curva ROC del modello sul rischio]({{ site.baseurl }}/assets/images/modello/mod_roc.png){: .img-fluid }

L'AUC è **0,668**: discreta, non altissima. Il valore regge su dati che il modello non ha mai
visto (**0,665** su un test set tenuto da parte, cross-validation fra 0,665 e 0,672), quindi non
è il frutto di un adattamento eccessivo. La lettura onesta è che con sole caratteristiche
**strutturali** (dove nasce il progetto, che cosa fa, quanto vale, chi lo finanzia) il segnale
c'è ma **non basta per un allarme operativo affidabile**. Servirebbero variabili di processo:
l'avanzamento dei pagamenti nel tempo, i passaggi amministrativi, i tempi delle gare.

# Il modello speculare: chi arriva in fondo

Stimare gli stessi fattori sulla probabilità di **concludere** il progetto restituisce l'immagine
allo specchio, come atteso. Il Mezzogiorno ha OR **0,46** sulla conclusione: a parità di tutto,
arrivare in fondo è molto meno probabile. I progetti sopra i 50 milioni concludono pochissimo
(OR 0,15) e i lavori pubblici meno degli acquisti (0,74), mentre entrambe le fonti di finanziamento
vanno nella direzione opposta: quota europea OR 1,87 e capitale privato OR 8,6. Quest'ultimo numero
è vistoso e va letto con la stessa cautela di prima: i progetti cofinanziati da privati sono quasi
tutti incentivi alle imprese, che si chiudono con la rendicontazione dell'investimento. Rischio e
conclusione restano comunque due facce dello stesso fenomeno, e il modello le legge in modo
coerente.

# In sintesi

Il verdetto sulla domanda di apertura: **il territorio pesa di per sé**. Al Sud le odds di
rischio sono quasi il triplo *a parità di tipo di intervento, tema, dimensione, fonti di
finanziamento e governance*, e il divario è **persistente**: presente in ogni ciclo, con intensità diverse.

Accanto al territorio il modello mette a fuoco un fattore che l'esplorazione non aveva isolato:
**il tipo di intervento**. Costruire opere ed erogare contributi a terzi rischia molto più che
acquistare beni o servizi. È una leva su cui, a differenza della geografia, si può intervenire
scrivendo diversamente i bandi. Nella stessa direzione va il **cofinanziamento privato**, che però
riduce il rischio solo là dove il privato finanzia il proprio investimento. Nel frattempo un
sospettato esce assolto: la **complessità di governance** non spiega i ritardi.

Un'avvertenza finale, la più importante: gli odds ratio sono **associazioni, non effetti
causali**. L'OR del Mezzogiorno non dice che «essere al Sud» produce il rischio: riassume
capacità amministrativa, contesto e prassi che si sommano nel territorio e che i dati di
OpenCoesione non permettono di separare. Che cosa farne, lo discutiamo nelle
[conclusioni]({{ site.baseurl }}/#cosa-fare).

Resta però una domanda che questo modello non affronta: non *quanto pesa* ciascun fattore, ma
**quanto lontano si può arrivare a prevedere** chi si incepperà. Se ne occupa il
[Random Forest]({{ site.baseurl }}/random-forest.html), che parte proprio dall'AUC 0,665
raggiunta qui.
