---
layout: default
title: "Text Analysis"
vega: true
show_sidetoc: true
header_type: hero 
header_img: assets/images/header.svg
header_title: "Text Analysis"
subtitle: "Le descrizioni dei progetti raccontano il loro esito?"
---

Analizziamo le etichette e i testi con cui i progetti sono descritti per capire se 
emergono parole, temi o tipi di intervento associati a una maggiore o minore 
probabilità di successo o ritardo.
{: .lead }

# Corpus e preprocessing

Per condurre questa analisi abbiamo analizzato le sintesi testuali di migliaia di progetti PNRR e OpenCoesione. 
Il linguaggio burocratico è spesso ripetitivo; per questo, dopo una pulizia iniziale, abbiamo rimosso le "stop-word di dominio", ovvero termini onnipresenti come *progetto, intervento, finanziamento, fondo*. 

Abbiamo così isolato il "cuore" semantico di ogni proposta: sono le parole distintive — quelle che descrivono l'oggetto specifico dell'azione — a rivelare i pattern di successo o di rischio che si nascondono dietro la burocrazia.

# Parole e temi ricorrenti

Confrontando il PNRR con lo storico di OpenCoesione, emerge un cambio di natura nel vocabolario dei progetti. 
Mentre in OpenCoesione il rischio era storicamente associato a una burocrazia tradizionale (es. *metanizzazione*, *dipartimento*), nel PNRR le sfide si sono spostate verso progetti legati al mondo accademico e alla ricerca (*politecnico*, *università*, *percorsi*).

D'altro canto, nel PNRR, abbiamo identificato un "vocabolario del successo": termini legati alla digitalizzazione (*piattaforma*, *api*, *cie*) sono i più forti predittori di progetti che procedono spediti.

<!-- Qui puoi inserire un grafico a barre (es. con Altair) che confronta le 10 parole più frequenti tra PNRR e OC -->
<div style="height: 400px">
<vegachart schema-url="{{site.baseurl}}/assets/charts/rischio_words_chart.json" style="width: 100%; height: 100%"></vegachart>
</div>

# Testo ed esito

Abbiamo addestrato un modello di Intelligenza Artificiale per vedere se le parole contenute nelle descrizioni potessero prevedere il rischio di un progetto. 
Il risultato è sorprendente: il nostro modello ha raggiunto un'**AUC di 0.853**. 

Questo significa che leggere la descrizione di un progetto è estremamente informativo. Le parole scelte per descrivere l'obiettivo non sono solo formali: sono indicatori reali della complessità che il progetto incontrerà sul campo.

# Controllo: è il testo o il tipo di progetto?

Un rischio comune in questo tipo di analisi è scambiare l'effetto del testo con quello del contesto (es. progetti al Sud vs Nord). 
Abbiamo quindi integrato il testo con i dati strutturati (territorio e missione). L'analisi dimostra che **il segnale testuale resiste**: il modo in cui un progetto viene descritto aggiunge valore predittivo indipendente. La semantica non è un riflesso della geografia, ma una dimensione aggiuntiva che ci aiuta a prevedere il futuro dei fondi.

# Indice di Rischio Storico: guardare al passato per prevedere il presente

Abbiamo creato un "ponte semantico" tra il PNRR e il passato di OpenCoesione. Per ogni progetto PNRR, il nostro algoritmo cerca i suoi 5 "gemelli storici": progetti che in passato avevano finalità identiche.
L'**Indice di Rischio Storico** che ne deriva ci dice quanto quel tipo di intervento sia stato problematico in passato.

<!-- Qui inserisci il grafico dell'Indice di Rischio per Missione PNRR -->
<div style="height: 400px">
<vegachart schema-url="{{site.baseurl}}/assets/charts/rischio_per_missione.json" style="width: 100%; height: 100%"></vegachart>
</div>

# Cosa emerge

La nostra analisi suggerisce che:
1. **La digitalizzazione è un fattore di stabilità:** i progetti orientati alla transizione digitale del PNRR mostrano i segnali di rischio più bassi.
2. **Le collaborazioni complesse sono fragili:** le missioni che coinvolgono attori multipli (es. Istruzione e Ricerca) mostrano un rischio storico maggiore, probabilmente a causa della complessità di coordinamento.
3. **Il linguaggio è un segnale:** l'attenzione alla precisione terminologica nelle descrizioni (es. piattaforme specifiche invece di descrizioni vaghe) correla fortemente con una migliore esecuzione.

Questi risultati offrono una nuova chiave di lettura per i decisori: non basta guardare ai budget, bisogna ascoltare il linguaggio dei progetti.
