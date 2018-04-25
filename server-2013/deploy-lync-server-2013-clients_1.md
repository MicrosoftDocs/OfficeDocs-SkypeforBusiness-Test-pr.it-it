---
title: Distribuire client di Lync Server 2013
TOCTitle: Distribuire client di Lync Server 2013
ms:assetid: 508e5dfa-588b-4289-81ce-2043c2d79e04
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204883(v=OCS.15)
ms:contentKeyID: 49300559
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuire client di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-19_

Dopo aver eseguito la migrazione degli utenti Lync Server 2013, eseguire le operazioni seguenti:

1.  Usare l'applicazione Client Version Filter nel nuovo server Lync Server 2013 per consentire l'accesso solo ai client con gli aggiornamenti più recenti installati.

2.  Se necessario, configurare le impostazioni di Criteri di gruppo necessarie per l'avvio automatico dei client. Per informazioni dettagliate, vedere [Configurazione dei criteri di avvio dei client in Lync Server 2013](lync-server-2013-configuring-client-bootstrapping-policies.md) nella documentazione relativa alla distribuzione. La configurazione di queste impostazioni è necessaria solo se si vogliono modificare i criteri esistenti di avvio automatico dei client oppure impostare nuovi criteri. Se non si intende configurare i criteri di avvio automatico dei client o si vogliono mantenere effettivi i criteri legacy, non sarà necessaria alcuna azione.

3.  Configurare altri criteri utente e client per specifici utenti o gruppi tramite il Pannello di controllo di Lync Server 2013, Lync Server 2013 Management Shell o entrambi. Per informazioni dettagliate, vedere [Impostazioni nuove e modificate per Lync 2013](lync-server-2013-new-and-changed-settings-for-lync-2013.md) nella documentazione relativa alla pianificazione.

4.  Distribuire la versione più recente dei client Lync Server 2013 oltre agli ultimi aggiornamenti cumulativi. Per informazioni dettagliate, vedere [Distribuzione di client e dispositivi in Lync Server 2013](lync-server-2013-deploying-clients-and-devices.md) nella documentazione relativa alla distribuzione.

5.  (Facoltativo) Se nell'organizzazione è necessaria la modalità privacy della presenza avanzata di Lync Server 2013, al termine della migrazione definire una regola dei criteri delle versioni dei client per impedire l'accesso a versioni precedenti dei client. Quindi, abilitare la modalità privacy della presenza avanzata.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Non abilitare la modalità privacy della presenza avanzata di Lync 2013 se tutti gli utenti di un determinato pool di server non dispongono delle versioni più recenti dei client installate.</td>
    </tr>
    </tbody>
    </table>

