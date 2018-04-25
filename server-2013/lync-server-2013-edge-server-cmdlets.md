---
title: Cmdlet per i server perimetrali
TOCTitle: Cmdlet per i server perimetrali
ms:assetid: 1a5427f4-a0d1-4652-8135-91333158ffc8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg415635(v=OCS.15)
ms:contentKeyID: 49299837
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlet per i server perimetrali

 

_**Ultima modifica dell'argomento:** 2013-10-07_

I server perimetrali consentono di estendere le funzionalità di Microsoft Lync Server 2013 agli utenti non connessi alla rete interna. Se ad esempio vi sono utenti remoti, ovvero utenti autenticati che eseguono l'accesso a Lync Server 2013 tramite Internet anziché tramite la rete interna, sarà necessario configurare un server perimetrale che esegua il servizio Lync Server Access Edge. I server perimetrali sono inoltre necessari se si desidera stabilire una federazione con un'altra organizzazione oppure se si desidera concedere ai propri utenti il diritto di comunicare con persone che dispongono di account presso un servizio di messaggistica istantanea pubblica come Yahoo\!, AOL o MSN.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Dal 1 settembre 2012, la licenza di sottoscrizione utenti per la connettività di messaggistica istantanea pubblica di Microsoft Lync (“PIC USL”) non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. I clienti con licenze attive potranno continuare a eseguire la federazione con Yahoo! Messenger fino alla data di chiusura del servizio. Giugno 2014 è la data di fine servizio annunciata per Yahoo! e AOL. Per informazioni dettagliate, vedere <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013</a>.</p></li>
<li><p>La licenza PIC USL è una licenza di sottoscrizione di tipo mensile per utente, richiesta per la federazione di Lync Server o Office Communications Server con Yahoo! Messenger. La capacità di Microsoft di fornire questo servizio dipende dal supporto offerto da Yahoo! e il contratto sottostante è in fase di chiusura.</p></li>
<li><p>Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti di tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze per utente/dispositivo in aggiunta alla licenza CAL Standard per Lync. La federazione con Skype verrà aggiunta a questo elenco, consentendo agli utenti di Lync di raggiungere centinaia di milioni di persone tramite messaggistica istantanea e comunicazioni vocali.</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Cmdlet per i server perimetrali

Di seguito è riportato un elenco dei cmdlet correlati direttamente alla gestione dei server perimetrali:

**Server perimetrale**

  -   
    [Get-CsAccessEdgeConfiguration](get-csaccessedgeconfiguration.md)

  -   
    [Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)

  -   
    [Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)

  -   
    [New-CsAVEdgeConfiguration](new-csavedgeconfiguration.md)

  -   
    [Remove-CsAVEdgeConfiguration](remove-csavedgeconfiguration.md)

  -   
    [Set-CsAVEdgeConfiguration](set-csavedgeconfiguration.md)

  -   
    [Test-CsAVEdgeConnectivity](test-csavedgeconnectivity.md)

  -   
    [Set-CsEdgeServer](set-csedgeserver.md)

## Vedere anche

#### Ulteriori risorse

[Blog di Lync Server PowerShell](http://go.microsoft.com/fwlink/?linkid=203150)

