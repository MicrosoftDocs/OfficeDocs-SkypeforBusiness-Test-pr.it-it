---
title: Ripristino di un server back-end Enterprise Edition con mirroring - Mirroring
TOCTitle: Ripristino di un server back-end Enterprise Edition con mirroring - Mirroring
ms:assetid: 4b3c8eae-6f1f-4377-b39b-6699e725c517
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945626(v=OCS.15)
ms:contentKeyID: 52062145
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ripristino di un server back-end Enterprise Edition con mirroring - Mirroring

 

_**Ultima modifica dell'argomento:** 2013-02-19_

In presenza di un server back-end Enterprise Edition in una configurazione con mirroring e se l'errore riguarda solo il mirror, seguire le procedure in questa sezione. Se l'errore coinvolge sia il database primario che il mirror, vedere [Ripristino di un Server Enterprise back-end](lync-server-2013-restoring-an-enterprise-edition-back-end-server.md). In caso di errore solo del database primario, vedere [Ripristino di un server back-end Enterprise Edition con mirroring - Principale](lync-server-2013-restoring-a-mirrored-enterprise-edition-back-end-server-primary.md). Se il problema si verifica nel database che ospita l'archivio di gestione centrale, vedere [Ripristino del server che ospita l'archivio di gestione centrale](lync-server-2013-restoring-the-server-hosting-the-central-management-store.md). Se si verifica un errore in un server membro Enterprise Edition che non è il server back-end, vedere [Ripristino di un server membro Enterprise Edition](lync-server-2013-restoring-an-enterprise-edition-member-server.md).

È consigliabile acquisire una copia dell'immagine del sistema prima di avviare il ripristino, per poterla utilizzare come punto di ripristino dello stato precedente in caso di problemi durante le operazioni di ripristino. È possibile acquisire la copia dell'immagine dopo l'installazione del sistema operativo e di SQL Server e ripristinare o registrare di nuovo i certificati.

## Per ripristinare un database mirror del server back-end Enterprise Edition

1.  Con un account utente membro del gruppo RTCUniversalServerAdmins accedere a un Front End Server.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Disinstallare il mirroring. Utilizzare innanzitutto il cmdlet seguente:
    
        Uninstall -CsMirrorDatabase -DatabaseType User -SqlServerFqdn <PrimaryServerFqdn> -SqlInstanceName <SQLInstance> -verbose
    
    Ad esempio:
    
        Uninstall -CsMirrorDatabase -DatabaseType User -SqlServerFqdn server4.contoso.com -SqlInstanceName archinst -verbose
    
    Eseguire questa operazione per tutti i tipi di database nel server.

4.  Creare un server pulito o nuovo con lo stesso nome di dominio completo (FQDN) (DB1.contoso.com) del computer in errore, installare il sistema operativo e quindi ripristinare o registrare di nuovo i certificati. Questo server opererà come nuovo mirror.

5.  Con un account utente membro del gruppo RTCUniversalServerAdmins accedere al nuovo server.

6.  Installare SQL Server 2012 o SQL Server 2008 R2 mantenendo gli stessi nomi delle istanze utilizzati prima dell'errore.

7.  Con un account utente membro del gruppo RTCUniversalServerAdmins accedere a un Front End Server.

8.  Utilizzare Generatore di topologie per installare il database mirror. Eseguire le operazioni seguenti:
    
      - Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.
    
      - Fare clic con il pulsante destro del mouse sul nodo Lync Server 2013, scegliere **Topologia** e quindi fare clic su **Installa database**.
    
      - Seguire le istruzioni della procedura guidata**Installa database**. Nella pagina **Creare database** selezionare i database che si desidera ricreare.
    
      - Seguire i vari passaggi della procedura guidata fino a quando non viene visualizzata la richiesta **Creare database mirror**. Selezionare il database che si desidera installare e completare il processo.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Anziché eseguire Generatore di topologie, è possibile utilizzare il cmdlet <strong>Install-CsMirrorDatabase</strong> per configurare il mirroring. Per informazioni dettagliate, vedere la documentazione di Lync Server Management Shell.</td>
        </tr>
        </tbody>
        </table>

