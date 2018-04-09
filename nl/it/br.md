---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-16"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Backup e ripristino
{: #br}

Un backup crittografato del database {{site.data.keyword.dashdbshort_notm}} completo viene eseguito una volta al giorno. Per il piano Flex Performance, sono conservate le istantanee dei backup degli ultimi 7 giorni. Per i piani SMP e MPP, vengono conservati gli ultimi 2 backup giornalieri.
{: shortdesc}

Nel piano Flex Performance, puoi pianificare i tuoi backup per essere eseguiti quando ti è più conveniente e puoi ripristinare il tuo database da una qualsiasi delle tue istantanee di backup conservate, in qualsiasi momento tu voglia. Il sistema si arresta durante il periodo di ripristino. Verrà inviata un'email per informarti che l'operazione di ripristino è stata completata.

Nel caso dei piani SMP e MPP, i backup conservati vengono utilizzati esclusivamente da IBM solo per scopi di ripristino del sistema nel caso di un'emergenza o un danno al sistema. Una richiesta per ripristinare il tuo database da un backup non è supportata. Puoi esportare i dati utilizzando gli strumenti Db2 come IBM Data Studio o utilizzando il comando **db2 export**. 
