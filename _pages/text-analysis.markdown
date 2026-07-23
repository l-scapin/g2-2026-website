---
layout: default
title: "Text Analysis"
vega: true
show_sidetoc: true
header_type: hero
header_img: assets/images/hero_text_analysis.jpg
header_img_position: center
header_title: "Text Analysis"
subtitle: "Le parole di un progetto dicono qualcosa sul suo destino?"
---

<!-- PAGINA IN PREPARAZIONE: l'analisi testuale sopra il Random Forest non è ancora stata
     eseguita. Qui ci sono la domanda, il metodo e il criterio di lettura, scritti PRIMA di
     vedere i risultati: è una garanzia contro il racconto costruito a posteriori. La sezione
     "I risultati" va riempita quando il notebook è pronto ed è formulata per reggere
     qualunque esito.
     ⚠️ La versione precedente di questa pagina era costruita sul PNRR, fuori dallo scope
     deciso il 18/07/2026, e conteneva nome e indirizzo di un'impresa privata associati a una
     previsione di fallimento al 100%: è stata sostituita. Copia conservata fuori dal repo.
     Regole editoriali: mai "causale", "persistente" e NON "strutturale", niente virgolettati
     inventati, nessun risultato pre-affermato. -->

<div class="full-width-wrapper">
    <img src="{{ site.baseurl }}/assets/images/header.svg" alt="sbd-pattern" class="full-width-image">
</div>

Finora abbiamo trattato ogni progetto come una riga di tabella: un territorio, un importo, un
tema, una natura. Ma ogni progetto porta con sé anche **una descrizione scritta da chi lo ha
proposto**. È l'unico punto in cui l'amministrazione racconta, con parole sue, che cosa intende
fare. La domanda di questa pagina è se in quelle parole ci sia informazione che le colonne non
contengono.
{: .lead }

<div class="def-box" markdown="1">
**Analisi in corso.** Questa pagina descrive la domanda, il metodo e il criterio con cui
leggeremo i risultati. I numeri arriveranno alla chiusura dell'analisi.
</div>

# La domanda {#domanda}

Il [Random Forest]({{ site.baseurl }}/random-forest.html) si ferma a **AUC 0,813** usando sette
caratteristiche strutturali. Sappiamo anche che una parte di quel risultato dipende dal
riconoscere il piano di finanziamento più che il progetto in sé. La domanda naturale è se il
**testo della descrizione** aggiunga qualcosa di diverso: non «quanto vale e dove nasce» ma
«che cosa dice di voler fare, e come lo dice».

L'ipotesi è ragionevole. Un progetto descritto in modo preciso e circoscritto racconta un'idea
già messa a fuoco; una descrizione generica e formulare può segnalare un intervento ancora da
definire. Ma è appunto un'ipotesi, e va misurata.

# Il metodo {#metodo}

**Il corpus è `OC_SINTESI_PROGETTO`**, la sintesi testuale dei progetti OpenCoesione. Solo
OpenCoesione: il PNRR resta fuori dal perimetro del progetto.

Il testo viene ripulito e trasformato in numeri con una vettorizzazione classica, poi le feature
testuali vengono affiancate a quelle strutturali già usate dagli altri modelli. Il confronto è
fra due Random Forest identici in tutto tranne che nell'input:

- il modello **con le sole variabili strutturali**, che è il nostro riferimento a 0,813;
- il modello **con testo e variabili strutturali insieme**.

La differenza fra i due, misurata **sugli stessi progetti tenuti fuori dall'addestramento**, è
il guadagno attribuibile al testo. È l'unica misura che conta: valutare il testo sui dati con cui
il modello è stato addestrato produce numeri lusinghieri e privi di significato.

# Le tre trappole che dobbiamo evitare {#cautele}

Sono dichiarate qui, prima di avere i risultati, perché sono esattamente i punti in cui
un'analisi testuale può auto-ingannarsi.

**Il testo che riscopre quello che già sappiamo.** Le descrizioni contengono spesso nomi di
programmi, di luoghi e di strumenti di finanziamento. Un modello che impara a riconoscere
«POR FESR Sicilia» dentro una sintesi non ha scoperto niente sul linguaggio: ha ritrovato per
un'altra strada il territorio e il ciclo, che sono già in tabella. Il guadagno del testo si
misura **in aggiunta** alle variabili strutturali, mai da solo.

**Le etichette travestite da testo.** Il tema sintetico e la natura dell'intervento sono
classificazioni, non prosa. Usarle come se fossero testo significa prevedere una colonna con se
stessa, e produce accuratezze altissime e prive di valore. Nel corpus entra solo la descrizione
libera.

**Il vocabolario che è solo un calendario.** Il linguaggio amministrativo cambia nel tempo: certi
termini appartengono a una stagione di programmazione, e i cicli hanno tassi di rischio molto
diversi fra loro. Un modello può quindi imparare a datare il progetto invece di capirlo. Va
verificato se il segnale testuale sopravvive **dentro un singolo ciclo**.

# I risultati {#risultati}

<div class="def-box" markdown="1">
**[SEZIONE DA COMPLETARE]**: qui andranno il guadagno del testo sul modello strutturale, i termini
più associati al rischio e alla conclusione, e l'esito dei tre controlli descritti sopra.
</div>

Le due letture possibili sono entrambe informative, e le dichiariamo adesso.

**Se il testo aggiunge poco**, la conclusione è che le descrizioni sono in larga parte
**linguaggio formulare**: dicono come si compila una domanda di finanziamento, non come andrà il
progetto. Sarebbe un risultato utile, perché ridimensiona un'idea molto diffusa.

**Se il testo aggiunge molto**, la domanda successiva diventa *quali* parole pesano, e lì serve
la massima prudenza: un termine associato al rischio non è una causa e non è una colpa. È il
segno che un certo tipo di intervento, descritto in un certo modo, storicamente si è inceppato
più spesso.

In nessuno dei due casi pubblicheremo previsioni riferite a progetti singoli riconoscibili. Un
modello che assegna una probabilità di fallimento a un intervento identificabile, con il nome
dell'ente o dell'impresa che lo realizza, non è un risultato di ricerca: è un giudizio su
soggetti reali basato su una correlazione. Le analisi di questa pagina restano aggregate.
