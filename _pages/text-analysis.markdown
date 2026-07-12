---
layout: default
title: "Text Analysis"
vega: true
show_sidetoc: true
header_type: hero
header_img: assets/images/header.svg
header_title: "Text Analysis"
subtitle: "Le parole con cui un progetto viene descritto anticipano il suo esito?"
---

Abbiamo letto le sintesi testuali di migliaia di progetti PNRR e OpenCoesione per capire
se, oltre ai numeri, anche il *modo in cui un progetto viene raccontato* contenga indizi
sulla probabilità che vada in ritardo.
{: .lead }

# Dalle parole ai temi

Le descrizioni ufficiali dei progetti sono scritte in un linguaggio molto burocratico e
ripetitivo: termini come *progetto*, *finanziamento* o *fondo* compaiono ovunque e non
raccontano nulla di specifico. Abbiamo quindi "pulito" i testi per far emergere le parole
davvero distintive di ciascun intervento — quelle che ne descrivono l'oggetto concreto.

# Il vocabolario del rischio cambia con il tempo

Confrontando OpenCoesione (il passato) con il PNRR (il presente), il tipo di rischio
raccontato dai testi è cambiato natura. In OpenCoesione il rischio era legato a una
burocrazia più tradizionale (termini come *dipartimento*, *metanizzazione*). Nel PNRR il
rischio si sposta invece su progetti legati al mondo accademico e alla ricerca (*percorsi*,
*partecipante*, *università*).

Al contrario, nel PNRR i progetti che citano la digitalizzazione — *piattaforma*, *CIE*,
*servizi digitali* — sono quelli che procedono più spediti: un segnale che la
transizione digitale, pilastro del Piano, sta funzionando bene sul campo.

<div style="height: 400px">
<vegachart schema-url="{{site.baseurl}}/assets/charts/rischio_words_chart.json" style="width: 100%; height: 100%"></vegachart>
</div>

# Le parole bastano per prevedere il ritardo?

Abbiamo verificato quanto le sole parole della sintesi progettuale siano in grado di
anticipare se un progetto rischia il ritardo. Il risultato: un modello basato sul testo
(insieme a un'informazione territoriale di base) individua correttamente il rischio in
circa **85 casi su 100**, contro il 68% di un modello che usa solo i dati strutturati
tradizionali (dimensione, ente attuatore, territorio).

In altre parole: **come viene descritto un progetto non è un dettaglio formale**. Le
parole scelte per raccontare l'obiettivo contengono informazioni reali sulla complessità
che il progetto incontrerà.

# Non è solo una questione di geografia

Un rischio tipico di questo genere di analisi è confondere l'effetto del testo con quello
del contesto — ad esempio, i progetti al Sud potrebbero semplicemente scrivere le sintesi
in modo diverso da quelli al Nord. Abbiamo quindi verificato il potere predittivo del testo
tenendo sotto controllo l'area geografica (Mezzogiorno vs resto d'Italia): **il segnale
testuale resta forte**. Il modo in cui un progetto viene descritto aggiunge informazione
utile, indipendente dalla sua localizzazione.

# Un indice di rischio basato sulla storia

Abbiamo provato a costruire un "ponte" tra il presente e il passato: per ogni progetto
PNRR, un algoritmo di ricerca semantica individua i suoi "gemelli storici" — i progetti
OpenCoesione con la sintesi più simile — e calcola quanti di questi gemelli sono finiti in
ritardo. Ne nasce un **Indice di Rischio Storico**: quanto quel *tipo* di intervento è
stato problematico in passato.

<div style="height: 400px">
<vegachart schema-url="{{site.baseurl}}/assets/charts/rischio_per_missione.json" style="width: 100%; height: 100%"></vegachart>
</div>

*Nota metodologica: questo indice è calcolato al momento su un campione di circa 1.000
progetti PNRR (l'elaborazione sull'intero dataset è in corso). Per alcune missioni con
pochissime osservazioni nel campione — in particolare Infrastrutture per la mobilità
sostenibile, Salute e REPowerEU — il valore è indicativo e potrà variare con l'analisi
completa; le missioni con più osservazioni (Digitalizzazione, Istruzione e ricerca,
Inclusione e coesione) offrono al momento un segnale più stabile.*

# Cosa emerge

1. **La digitalizzazione è un fattore di stabilità.** I progetti orientati alla
   transizione digitale (Missione 1) mostrano, storicamente, l'indice di rischio più
   basso: interventi basati su standard tecnologici definiti sembrano più resilienti.

2. **Istruzione e ricerca è la missione storicamente più a rischio** tra quelle con un
   numero di osservazioni sufficiente. Un'ipotesi plausibile — da verificare con analisi
   più approfondite — è che si tratti spesso di investimenti a lungo termine con
   protocolli di verifica più rigidi, che tendono ad allungare i tempi.

3. **Il linguaggio è un segnale predittivo utile.** Il fatto che il testo aggiunga
   capacità predittiva rispetto ai soli dati strutturati suggerisce che la chiarezza con
   cui un progetto viene descritto — ad esempio il riferimento a standard tecnici precisi
   invece che a formule generiche — è legata a una migliore esecuzione.

Questi risultati suggeriscono che, per mitigare il rischio, non basta guardare ai budget:
serve anche una maggiore standardizzazione del linguaggio progettuale, specialmente per le
missioni a vocazione accademica e di ricerca.


