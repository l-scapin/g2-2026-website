---
layout: default
title: "Modello"
vega: true
show_sidetoc: true
header_type: hero #base, post, hero, image, splash
header_img: assets/images/header.svg
header_title: "Il modello predittivo"
subtitle: "Territorio o dimensione: chi pesa di più nel rischio?"
---

L'EDA lascia aperta la domanda decisiva: il divario Nord-Sud conta *di per sé*, o riflette la
dimensione, il ciclo e il tema dei progetti? Qui un modello impara a riconoscere i progetti a
rischio e ci dice quali variabili pesano davvero. **[DA COMPLETARE — Notebook 02]**
{: .lead }

<!-- NOTA METODO: la Random Forest dà importanza delle variabili, non effetti "a parità di
     condizioni" (+X punti, odds ratio). Per una frase del tipo "a parità di dimensione e ciclo,
     il Sud ha +X punti di rischio" affiancare una regressione logistica semplice. -->
<!-- Scrivere l'interpretazione in modo che regga entrambi gli esiti (territorio rilevante o no):
     lo slot corrispondente in conclusions.html è già impostato così. -->

# Feature e preparazione del dataset

<!-- Variabili predittive, gestione dei mancanti, train/test split. -->

# Addestramento e validazione

<!-- Iperparametri, metriche (accuracy, ROC/AUC), curva ROC. -->

<!-- ---- SEGNAPOSTO GRAFICO (Altair/Vega) ----
<div style="height: 400px">
<vegachart schema-url="{{site.baseurl}}/assets/charts/NOME_FILE.json" style="width: 100%; height: 100%"></vegachart>
</div>
-->

# Importanza delle variabili

<!-- Feature importance / SHAP: quali variabili pesano di più. -->

<!-- ---- SEGNAPOSTO GRAFICO ----
<div style="height: 400px">
<vegachart schema-url="{{site.baseurl}}/assets/charts/NOME_FILE.json" style="width: 100%; height: 100%"></vegachart>
</div>
-->

# Interpretazione

<!-- Cosa dice il modello rispetto alle domande del progetto. -->
