---
title: 'Lync Server 2013: Esportare un file di configurazione di route vocali'
TOCTitle: Esportare un file di configurazione di route vocali
ms:assetid: 02ce922d-9ca8-4513-b09f-9de51f5c5bdc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398081(v=OCS.15)
ms:contentKeyID: 49299503
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Esportare un file di configurazione di route vocali in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Se si desidera salvare la configurazione del routing vocale senza pubblicarla, eseguire questa procedura per utilizzare i comandi di esportazione e importazione della configurazione del Pannello di controllo di Lync Server per salvare e recuperare uno snapshot della configurazione del routing vocale. Se si importa un file di configurazione del routing vocale (con estensione vcfg) e nel frattempo sono state apportate modifiche alla configurazione del routing vocale nel server, nelle pagine nel gruppo **Routing vocale** del Pannello di controllo di Lync Server verrà indicato che esistono modifiche del routing vocale di cui non è stato eseguito il commit. Tali modifiche costituiscono le differenze tra le due configurazioni di cui deve essere eseguita la riconciliazione.

Se sono state apportate modifiche di cui non è stato eseguito il commit alle impostazioni di una pagina all'interno del gruppo, le modifiche vengono salvate nel file di configurazione vocale esportato ( con estensione vcfg). Questo consente di modificare la configurazione del routing vocale durante più sessioni prima di pubblicare le modifiche.

## Per esportare una configurazione di routing vocale

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale** .

4.  Scegliere **Esporta configurazione** dal menu **Azioni** .

5.  Specificare un percorso e un nome di file e quindi fare clic su **Salva** .

## Vedere anche

#### Attività

[Importare un file di configurazione di route vocali in Lync Server 2013](lync-server-2013-import-a-voice-route-configuration-file.md)

