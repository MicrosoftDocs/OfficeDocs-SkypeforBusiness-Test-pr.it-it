---
title: 'Lync Server 2013: Avviare servizi nei server'
TOCTitle: Avviare servizi nei server
ms:assetid: fa26eaed-0529-4f32-9f3f-f32c4bd4b1c8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413059(v=OCS.15)
ms:contentKeyID: 49302541
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Avviare servizi nei server per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-09-03_

Per eseguire questa procedura, è necessario accedere come utente membro del gruppo RTCUniversalServerAdmins o disporre della delega delle autorizzazioni appropriate. Per informazioni dettagliate sulla delega delle autorizzazioni, vedere l'argomento [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

Dopo aver installato l'archivio di configurazione locale nei server, installato i componenti di Lync Server 2013 e configurato un certificato su un Front End Server o Front End Server, è necessario avviare i servizi di Lync Server 2013 sul server. Eseguire la procedura seguente per avviare i servizi su ogni Front End Server nella distribuzione.

## Per avviare i servizi su un server Standard Edition o Front End

1.  In Distribuzione guidata di Lync Server nella pagina **Lync Server 2013** fare clic su **Esegui** accanto a **Passaggio 4: Avvia servizi** .

2.  Nella pagina **Avvia servizi** fare clic su **Avanti** per avviare i servizi di Lync Server sul server.

3.  Nella pagina **Esecuzione comandi in corso** dopo aver avviato correttamente tutti i servizi fare clic su **Fine** .
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Il comando di avvio dei servizi sul server rappresenta il massimo sforzo per l'avvio effettivo dei servizi, ma potrebbe non riflettere lo stato effettivo del servizio. È consigliabile effettuare il passaggio <strong>Stato servizio (facoltativo)</strong> immediatamente dopo <strong>Avvia servizi</strong> per aprire Microsoft Management Console (MMC) e verificare che i servizi siano stati avviati correttamente. Se qualsiasi servizio di Lync Server non viene avviato, è possibile fare clic con il pulsante destro del mouse su tale servizio in MMC e quindi scegliere <strong>Avvia</strong> .</td>
    </tr>
    </tbody>
    </table>

