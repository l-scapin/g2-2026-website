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

Il [Random Forest]({{ site.baseurl }}/random-forest.html) ha raggiunto un'affidabilità predittiva eccellente utilizzando esclusivamente dati strutturati: importi, localizzazione, tipologia ed enti coinvolti. Ma nei database di OpenCoesione esiste un'altra colonna, l'unica in cui l'amministrazione proponente racconta con parole sue che cosa intende fare: la **sintesi del progetto**. 

La domanda a cui risponde questa sezione è: c'è un'informazione utile in quelle parole che le tabelle non riescono a catturare? E soprattutto, aggiungere l'analisi del linguaggio permette di prevedere il rischio con ancora più precisione?
{: .lead }

<div class="def-box" style="margin: 25px 0;">
  <p class="def-box__label">Il verdetto in sintesi</p>
  <h4>Il testo aggiunge poco, ma quel poco è reale</h4>
  <p>L'integrazione dell'analisi testuale migliora le capacità del modello predittivo, portando un guadagno netto e solido di <strong>+1,2 punti percentuali di affidabilità</strong>. È un incremento modesto, ma che sopravvive a test di controllo severissimi. Gran parte del "linguaggio" usato nei progetti è in realtà costituito da formule burocratiche o da "bandi fotocopia": riconoscerli significa scoprire da quale scrivania arriva il progetto, non valutarne le caratteristiche. Ma una volta ripulito da questi effetti, il linguaggio rivela davvero quali tematiche tendono a incepparsi più di frequente.</p>
</div>

# Il primo ostacolo: il corpus non è il dataset

Prima di analizzare le parole, conviene contarle. A differenza dei dati finanziari, la descrizione del progetto è un campo facoltativo. Su oltre 200.000 progetti analizzati, **solo il 52,2% possiede un testo** (107.988 progetti). 

E questa copertura non è distribuita a caso. I cicli di programmazione 2000-2006 e 2014-2020 hanno descrizioni per quasi tutti i progetti, mentre i cicli 2007-2013 e 2021-2027 sono quasi vuoti (rispettivamente 14,4% e 5,5% di copertura). Di fatto, analizzare il testo significa studiare in gran parte il ciclo 2014-2020.

<figure class="fig-home">
  <img src="{{ site.baseurl }}/assets/images/ta_copertura_testo.png"
       alt="Grafico a barre sulla copertura del corpus testuale">
  <figcaption>
    La copertura non è uniforme tra i cicli di programmazione. Due cicli sono quasi completi, due quasi vuoti.
  </figcaption>
</figure>

Inoltre, applicando gli algoritmi di lemmatizzazione (la tecnica che riduce le parole alla loro radice, trasformando "realizzazione" e "realizzato" nel verbo "realizzare"), è emersa un'ulteriore anomalia: **5.605 descrizioni non contenevano nemmeno una parola reale**. 
La stringa di gran lunga più utilizzata era `....` (inserita in quasi 4.500 progetti), seguita da refusi o segni di punteggiatura come `ND` o `---`. Non si trattava di descrizioni brevi, ma di "segnaposti": testo mancante travestito da testo presente, inserito solo per aggirare i controlli dei form informatici. 

Eliminando questi casi, il nostro *corpus* testuale si restringe a circa **102.000 descrizioni reali**. L'affidabilità del Random Forest sulle variabili strutturali valutata *solo su questo sottoinsieme* è pari a **0,799** (AUC). **Questo è il numero da battere**.

# Pulire il burocratese per trovare il segnale

Un algoritmo non "legge" le frasi, ma analizza le frequenze delle parole. Per evitare che il modello impari semplicemente il "burocratese" o i nomi delle amministrazioni locali, abbiamo filtrato tre grandi famiglie di termini, rimuovendo circa il 10,5% delle parole totali:

1. **Il burocratese onnipresente:** Parole come `progetto`, `intervento`, `attività`, o `prevedere`. Sono termini presenti in ogni descrizione, non discriminano il rischio ma inquinano le frequenze.
2. **Il lessico del finanziamento:** Termini come `euro`, `bando`, `FESR`, `regione` o `ministero`. Se il modello impara questi nomi, sta semplicemente riconoscendo l'amministrazione di origine, un dato che già possediamo in formato tabellare.
3. **Il rumore:** Forme giuridiche (`srl`, `spa`), toponomastica (`via`, `piazza`) o l'inglese dei progetti Interreg (`the`, `and`).

Una parola chiave che abbiamo invece **deciso di mantenere è `comune`**. Non è un riempitivo burocratico: ci dice *chi* sta attuando il progetto (un piccolo ente locale invece di una grande azienda o regione) ed è una delle informazioni più concrete che si possano estrarre.

# Unire numeri e parole: l'identikit dei bandi fotocopia

Per combinare il linguaggio con i dati strutturati, abbiamo calcolato un **"punteggio testuale"** per ogni progetto e lo abbiamo fornito in pasto al Random Forest come una nuova colonna aggiuntiva.

Il risultato iniziale è parso straordinario: **il modello è balzato da 0,799 a 0,832 di accuratezza (+3,2 punti)**. Ma da dove arriva un miglioramento così marcato? È il linguaggio o c'è un trucco?

Proprio come avevamo scoperto esplorando le anomalie della `QUOTA_UE` nella regressione, il modello è bravissimo a riconoscere i "cloni". Contando i testi, abbiamo scoperto che **il 23% dei progetti nel gruppo di test possedeva una descrizione identica parola per parola a un progetto del gruppo di addestramento**. 
La descrizione più diffusa (*"2-b - reinserimento di giovani 15-18enni in percorsi formativi"*) compariva perfettamente identica in ben 656 progetti. 

Il modello non stava "comprendendo" un rischio introco nelle parole: stava semplicemente riconoscendo la descrizione di uno specifico bando amministrativo duplicata centinaia di volte.

Per stimare il valore reale del linguaggio, abbiamo sottoposto l'algoritmo a due controlli incrociati severissimi:
1. **Lo split per testo unico:** Abbiamo vietato all'algoritmo di valutare descrizioni che aveva già visto.
2. **L'isolamento di un singolo ciclo:** Abbiamo limitato l'analisi al solo ciclo 2014-2020, per evitare che l'algoritmo si orientasse semplicemente cercando di "datare" il progetto usando parole vecchie o nuove.

Superati entrambi gli ostacoli, il testo continua a fornire un vantaggio predittivo netto: **+1,2 punti percentuali (da 0,829 a 0,841)**. Il testo aggiunge poco, ma quel poco è informazione reale che le otto variabili di tabella non riescono a cogliere.

# Le parole del rischio

Una volta dimostrato che il linguaggio ha un peso, abbiamo cercato le parole maggiormente associate al rischio di ritardo o blocco. Anche in questo caso, le classifiche grezze raccontano molto della struttura della Pubblica Amministrazione.

Senza applicare alcun filtro, in cima alle parole più "pericolose" troviamo `xylella`, `fastidiosa`, `olivicole` e `infetta` (tutte con un rischio del 98-100%). Sono termini presenti in quasi 300 progetti. Sembra un segnale forte, ma esplorando i dati si scopre che **provengono da una sola descrizione distinta fotocopiata 276 volte**. Non è una parola pericolosa: è un singolo bando regionale. 
Tra le parole più "sicure" (rischio vicino allo 0%) svettano stringhe prive di senso come `aaa`, `soco`, o `lainiziativa`. Si tratta di refusi di chi ha caricato i dati. E il fatto che un banale refuso identifichi la probabilità di completare un progetto è la prova definitiva che **il modello impara a profilare la scrivania di provenienza, non la qualità dell'opera**.

<figure class="fig-home">
  <img src="{{ site.baseurl }}/assets/images/ta_termini_bandi.png"
       alt="Grafico sui termini fotocopia associati ai bandi">
  <figcaption>
    In cima alle classifiche grezze non ci sono parole, ma bandi fotocopia e refusi d'ufficio.
  </figcaption>
</figure>

Per capire quali siano le reali tematiche problematiche, abbiamo imposto una soglia rigorosa: mostrare solo i termini che compaiono in **almeno 100 descrizioni distinte**, scartando manualmente acronimi e toponimi.

<figure class="fig-home">
  <img src="{{ site.baseurl }}/assets/images/figure/ta_termini_rischio.png"
       alt="Le parole agli estremi del rischio ripulite dai bandi fotocopia">
  <figcaption>
    L'identikit semantico del rischio dopo aver rimosso i bandi clonati.
  </figcaption>
</figure>

La classifica finale depurata conferma alcune delle tendenze che avevamo individuato fin dai primi clustering:
* Le parole che più trascinano la previsione verso il **rischio** (dai 27 ai 52 punti sopra la media) sono legate all'imprenditoria e alla ricerca pubblica: `dipartimento`, `attivi`, `investimenti`, `medie` e `piccole` (aziende), `videosorveglianza`, `scienze`. 
* I termini più associati alla **sicurezza** e alla puntualità (circa 30 punti sotto la media) riguardano la scuola, la formazione e i passaggi burocratici formali: `rendicontazione`, `diploma`, `classe`, `triennale`, `direttiva`, `avvio`.

*(Nota di metodo: Un termine associato al rischio non è una "causa" del ritardo. È il segnale statistico che un certo tipo di intervento, descritto in quel determinato modo, storicamente ha incontrato più ostacoli degli altri).*