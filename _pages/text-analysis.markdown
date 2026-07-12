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
probabilità di successo o di stallo.
{: .lead }

# Corpus e preprocessing

Per condurre questa analisi abbiamo studiato le sintesi testuali di decine di migliaia di progetti PNRR e OpenCoesione. 
Il linguaggio amministrativo è spesso standardizzato; per questo, dopo una pulizia iniziale del testo, abbiamo filtrato attivamente le "stop-word di dominio", rimuovendo termini onnipresenti e neutri come *progetto, intervento, finanziamento, comune*. 

Abbiamo così isolato il "cuore" semantico di ogni proposta: sono le parole distintive — quelle che descrivono l'oggetto specifico dell'azione — a rivelare i pattern nascosti dietro la burocrazia.

# Parole e temi ricorrenti

Confrontando i due programmi, emerge un salto generazionale nel "vocabolario del rischio". 
Nello storico di OpenCoesione, i progetti più a rischio erano associati alla burocrazia tradizionale (*dipartimento*, *imposta*) e agli interventi fisici o di welfare (*metanizzazione*, *servizio civile*). Nel PNRR, i termini di allerta si spostano sull'ambito formativo e accademico (*percorsi*, *politecnico*, *università studio*, *partecipante*).

D'altro canto, il PNRR vanta un chiarissimo "vocabolario del successo". I termini che abbattono maggiormente il rischio sono tutti legati alla transizione digitale: *piattaforma, cie (Carta d'Identità Elettronica), api, cms*.

<!-- Grafico Parole -->
<div style="height: 400px">
<vegachart schema-url="{{site.baseurl}}/assets/charts/rischio_words_chart.json" style="width: 100%; height: 100%"></vegachart>
</div>

# Testo ed esito

Ma il testo ha un reale potere predittivo? Abbiamo addestrato un modello di Intelligenza Artificiale per scoprirlo. 
Il risultato è eccellente: il nostro modello semantico ha raggiunto un'**AUC di 0.853** nell'identificare i progetti a rischio. 

Questo significa che leggere la descrizione di un progetto è estremamente informativo. Le parole scelte non sono una mera formalità per ottenere i fondi: sono indicatori accurati della reale complessità che il progetto incontrerà sul campo.

# Controllo: è il testo o il tipo di progetto?

Un errore comune nell'analisi testuale è confondere l'effetto delle parole con quello del contesto (es. progetti al Sud rispetto a quelli al Nord). 
Abbiamo quindi eseguito una *Feature Union*, integrando la matrice semantica con i dati strutturati (es. territorio). L'analisi dimostra che **il segnale testuale resiste e innalza le performance del modello**: il modo in cui un progetto è descritto aggiunge un valore predittivo indipendente e non è una semplice ombra della sua geografia.

# Indice di Rischio Storico: guardare al passato per prevedere il presente

Per tradurre queste stime in un indicatore concreto, abbiamo creato un "ponte semantico" tra il PNRR e i dati certificati di OpenCoesione. 
Dato un campione rappresentativo di 10.000 progetti PNRR, il nostro algoritmo ha cercato per ciascuno i suoi 5 "gemelli storici", ovvero i progetti passati più simili testualmente. La percentuale di fallimento di questi gemelli ha generato un **Indice di Rischio Storico** per il PNRR.

<!-- Grafico Missioni -->
<div style="height: 400px">
<vegachart schema-url="{{site.baseurl}}/assets/charts/rischio_per_missione.json" style="width: 100%; height: 100%"></vegachart>
</div>

# Due storie a confronto: proiezioni di successo e di rischio

Per rendere concreto l'algoritmo, abbiamo estratto due progetti-simbolo dal nostro dataset. Guardando al passato, il nostro motore di ricerca ha individuato le traiettorie più probabili per questi due interventi.

**🔴 Il progetto a Rischio**
* **Missione:** Salute
* **Sintesi:** *VIALE PICENO -MILANO*VIALE PICENO*INTERVENTO DI MANUTENZIONE STRAORDINARIA PER REALIZZAZIONE CASA DELLA COMUNITA'*
* **Indice di Rischio Storico:** 100.0%
> Questo tipo di descrizione si allinea a progetti storici di OpenCoesione che, nella totalità dei casi esaminati dal modello, hanno subito forti ritardi, probabilmente legati alla complessità degli interventi strutturali in contesti urbani densi.

**🟢 Il progetto di Successo**
* **Missione:** Istruzione e ricerca
* **Sintesi:** *Università degli Studi di VERONA*Territorio nazionale*REALIZZAZIONE DEGLI OBIETTIVI INDICATI NEL PROGRAMMA DI RICERCA*
* **Indice di Rischio Storico:** 0.0%
> Al contrario, questo intervento utilizza un lessico di tipo programmatico che il nostro modello associa alla puntualità. I suoi "gemelli" storici in OpenCoesione si sono conclusi regolarmente.


# Cosa emerge

La nostra analisi semantica, incrociata con l'indagine esplorativa (EDA), ci permette di concludere che:

1. **La digitalizzazione è un fattore di stabilità:** i progetti orientati alla transizione digitale (M1) mostrano l'Indice di Rischio Storico più basso (~25%). Le descrizioni tecniche e standardizzate (*piattaforma, api*) si traducono in una messa a terra più sicura.
2. **Le transizioni "fisiche" sono le più complesse:** le missioni legate alla transizione ecologica (Rivoluzione Verde) o energetica (REPowerEU) registrano i rischi storici più alti (rispettivamente 48% e 76%). Anche in passato (vedi la parola *metanizzazione* in OC) i progetti con impatto fisico sul territorio tendono ad accumulare forti ritardi, indipendentemente dal numero di attori coinvolti.
3. **Il linguaggio è un segnale d'allarme:** l'accuratezza semantica predice il rischio con un'efficacia (AUC 0.853) superiore a quella delle sole variabili strutturali. La chiarezza progettuale iniziale è, a tutti gli effetti, la prima garanzia di completamento di un'opera.