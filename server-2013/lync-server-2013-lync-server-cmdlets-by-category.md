---
title: Cmdlet di Lync Server 2013 per categoria
TOCTitle: Cmdlet di Lync Server 2013 per categoria
ms:assetid: 4ce274d7-b0ec-40b8-b85e-9a0613916ffb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398306(v=OCS.15)
ms:contentKeyID: 49300484
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlet di Lync Server 2013 per categoria

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Microsoft Lync Server 2013 viene fornito con quasi 550 cmdlet specifici per consentire agli amministratori di gestire Lync Server dalla riga di comando. È possibile accedere ai cmdlet da Lync Server Management Shell. È possibile recuperare informazioni della Guida relative a un cmdlet direttamente dalla riga di comando digitando un comando simile al seguente:

    Get-Help New-CsVoicePolicy -Full

Il comando precedente consente di recuperare le informazioni della Guida disponibili per il cmdlet **New-CsVoicePolicy**. Sostituire il riferimento a **New-CsVoicePolicy** con il nome del cmdlet per cui si desidera recuperare la Guida.

Per recuperare un elenco completo dei cmdlet disponibili per la gestione di Microsoft Lync Server 2013, digitare il comando seguente al prompt dei comandi di Lync Server Management Shell:

    Get-Command * -Module Lync -CommandType cmdlet

In caso di dubbi sui cmdlet necessari, è disponibile anche un elenco di cmdlet suddivisi in categorie, con relativi argomenti della Guida. Si noterà che alcuni cmdlet compaiono in più di una categoria, ma si tratta di un risultato intenzionale perché significa che sono applicabili a più aree del prodotto. Quello che segue è un elenco delle categorie:

## Argomenti della sezione


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-user-management-cmdlets.md">Cmdlet per la gestione degli utenti</a></p></td>
<td><p><a href="lync-server-2013-voice-application-cmdlets.md">Cmdlet per le applicazioni vocali</a></p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-client-management-cmdlets.md">Cmdlet per la gestione client</a></p></td>
<td><p><a href="lync-server-2013-advanced-enterprise-voice-cmdlets.md">Cmdlet per VoIP aziendale avanzato</a></p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-im-and-presence-cmdlets.md">Cmdlet per la messaggistica istantanea e la presenza</a></p></td>
<td><p><a href="lync-server-2013-pstn-connectivity-cmdlets.md">Cmdlet per la connettività PSTN</a></p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-conferencing-cmdlets.md">Cmdlet per le conferenze</a></p></td>
<td><p><a href="lync-server-2013-phones-and-devices-cmdlets.md">Cmdlet per telefoni e dispositivi</a></p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-infrastructure-and-deployment-cmdlets.md">Cmdlet per l'infrastruttura e la distribuzione</a></p></td>
<td><p><a href="lync-server-2013-migration-and-coexistence-cmdlets.md">Cmdlet per la migrazione e la coesistenza</a></p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-security-cmdlets.md">Cmdlet per la sicurezza</a></p></td>
<td><p><a href="lync-server-2013-lync-server-management-shell-configuration-cmdlets.md">Cmdlet per la configurazione di Lync Server Management Shell</a></p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-server-roles-and-services-cmdlets.md">Cmdlet per i servizi e i ruoli del server</a></p></td>
<td><p><a href="lync-server-2013-mobility-cmdlets.md">Cmdlet per dispositivi mobili</a></p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-application-management-cmdlets.md">Cmdlet per la gestione delle applicazioni</a></p></td>
<td><p><a href="lync-server-2013-persistent-chat-server-cmdlets.md">Cmdlet del server chat persistente</a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/en-us/powershell/module/skype/">Cmdlet per la federazione e l'accesso esterno in Lync Server 2013</a></p></td>
<td><p><a href="lync-server-2013-centralized-logging-cmdlets.md">Cmdlet di registrazione centralizzata</a></p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-enterprise-voice-cmdlets.md">Cmdlet per VoIP aziendale</a></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Ulteriori risorse

[Blog di PowerShell per Lync Server](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x410)

