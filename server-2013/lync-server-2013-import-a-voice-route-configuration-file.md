---
title: 'Lync Server 2013: Importare un file di configurazione di route vocali'
TOCTitle: Importare un file di configurazione di route vocali
ms:assetid: 4bac05e5-ed8b-4f10-96b0-b8a65ff356ec
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398301(v=OCS.15)
ms:contentKeyID: 49300457
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Importare un file di configurazione di route vocali in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Se si desidera salvare la configurazione del routing vocale senza pubblicarla, eseguire questa procedura per utilizzare i comandi di esportazione e importazione della configurazione del Pannello di controllo di Lync Server per salvare e recuperare uno snapshot della configurazione del routing vocale. Se si importa un file di configurazione del routing vocale (con estensione vcfg) e nel frattempo sono state apportate modifiche alla configurazione del routing vocale nel server, nelle pagine nel gruppo **Routing vocale** del Pannello di controllo di Lync Server verrà indicato che esistono modifiche del routing vocale di cui non è stato eseguito il commit. Tali modifiche costituiscono le differenze tra le due configurazioni di cui deve essere eseguita la riconciliazione.

Se sono state apportate modifiche di cui non è stato eseguito il commit alle impostazioni di una pagina all'interno del gruppo, le modifiche vengono salvate nel file di configurazione vocale esportato ( con estensione vcfg). Questo consente di modificare la configurazione del routing vocale durante più sessioni prima di pubblicare le modifiche.

## Per importare una configurazione di routing vocale

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale** .

4.  Scegliere **Importa configurazione** dal menu **Azioni** .

5.  Trovare il file di configurazione che si desidera importare e quindi fare clic su **Apri** .

6.  Fare clic su **Commit** e quindi su **Salva tutto** .
    

    > [!NOTE]
    > Ogni volta che si importa un file di configurazione vocale, è necessario usare il comando <STRONG>Salva tutto</STRONG> per pubblicare la modifica di configurazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013</A> nella documentazione relativa alle operazioni.



## Vedere anche

#### Attività

[Esportare un file di configurazione di route vocali in Lync Server 2013](lync-server-2013-export-a-voice-route-configuration-file.md)  
[Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)

