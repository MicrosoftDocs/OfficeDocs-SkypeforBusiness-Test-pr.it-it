---
title: 'Lync Server 2013: Esportazione e importazione della configurazione di route vocali'
TOCTitle: Esportazione e importazione della configurazione di route vocali
ms:assetid: c9b78622-5725-43b0-9ee1-5b82b1e1c8eb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398836(v=OCS.15)
ms:contentKeyID: 49301942
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Esportazione e importazione della configurazione di route vocali in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Se si desidera salvare la configurazione del routing vocale senza pubblicarla, eseguire questa procedura per utilizzare i comandi di esportazione e importazione della configurazione del Pannello di controllo di Lync Server per salvare e recuperare uno snapshot della configurazione del routing vocale. Se si importa un file di configurazione del routing vocale (con estensione vcfg) e nel frattempo sono state apportate modifiche alla configurazione del routing vocale nel server, nelle pagine nel gruppo **Routing vocale** del Pannello di controllo di Lync Server verrà indicato che esistono modifiche del routing vocale di cui non è stato eseguito il commit. Tali modifiche costituiscono le differenze tra le due configurazioni di cui deve essere eseguita la riconciliazione.

> [!important]  
> Se sono state apportate modifiche di cui non è stato eseguito il commit alle impostazioni di una pagina all'interno del gruppo <strong>Routing vocale</strong> , le modifiche vengono salvate nel file di configurazione vocale esportato ( con estensione vcfg). In questo modo è possibile modificare la configurazione del routing vocale durante più sessioni del Pannello di controllo di Lync Server prima di pubblicare le modifiche.

## Argomenti della sezione

  - [Esportare un file di configurazione di route vocali in Lync Server 2013](lync-server-2013-export-a-voice-route-configuration-file.md)

  - [Importare un file di configurazione di route vocali in Lync Server 2013](lync-server-2013-import-a-voice-route-configuration-file.md)

## Sezioni correlate

