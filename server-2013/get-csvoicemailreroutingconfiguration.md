---
title: Get-CsVoicemailReroutingConfiguration
TOCTitle: Get-CsVoicemailReroutingConfiguration
ms:assetid: 25e401eb-6a84-468f-b0eb-5b794f20b5bc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425732(v=OCS.15)
ms:contentKeyID: 49299958
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoicemailReroutingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera le impostazioni che forniscono i numeri di telefono della rete PSTN (Public Switched Telephone Network) per accedere alle funzionalità Messaggistica unificata di Exchange Accesso sottoscrittore e Operatore automatico. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsVoicemailReroutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsVoicemailReroutingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

In questo esempio vengono recuperate tutte le impostazioni di configurazione del rerouting della segreteria telefonica definite in questa distribuzione di Lync Server. Se ad esempio sono presenti tre succursali in cui viene distribuito Survivable Branch Appliance, questo comando restituirà tre insiemi di configurazioni del rerouting della segreteria telefonica.

    Get-CsVoicemailReroutingConfiguration

## ESEMPIO 2

In questo esempio vengono recuperate le impostazioni di configurazione del rerouting della segreteria telefonica per il sito BranchOffice\_Portland.

    Get-CsVoicemailReroutingConfiguration -Identity site:BranchOffice_Portland

## ESEMPIO 3

In questo esempio vengono recuperate tutte le impostazioni del rerouting della segreteria telefonica per tutti i siti i cui nomi iniziano con la stringa BranchOffice (ad esempio, BranchOffice\_Portland, BranchOffice\_Sacramento).

    Get-CsVoicemailReroutingConfiguration -Filter *:BranchOffice*

## ESEMPIO 4

In questo esempio vengono recuperate tutte le configurazioni del rerouting della segreteria telefonica non abilitate. La prima parte di questo comando è una chiamata al cmdlet **Get-CsVoicemailReroutingConfiguration**, che recupera una raccolta di tutte le configurazioni del rerouting della segreteria telefonica. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** circoscrive la raccolta per includere solo le configurazioni in cui la proprietà Enabled è uguale a (-eq) False.

    Get-CsVoicemailReroutingConfiguration | Where-Object {$_.Enabled -eq $False}

## Descrizione dettagliata

Questo cmdlet recupera le impostazioni che determinano il punto in cui vengono reindirizzate le chiamate di Accesso sottoscrittore e di Operatore automatico quando non è disponibile la connettività IP da Lync Server nel sito di succursale con il server Messaggistica unificata di Exchange posizionato nel data center.

Operatore automatico e Accesso sottoscrittore sono funzionalità della Messaggistica unificata di Exchange. La funzionalità Operatore automatico consente il riconoscimento vocale e il controllo della composizione a toni (DTMF, Dual-Tone Multifrequency) per permettere ai chiamanti esterni di spostarsi nel sistema telefonico della società per raggiungere il dipendente o il reparto desiderato oppure, nella modalità di sola ricezione dei messaggi, per accettare messaggi per gli utenti. È consigliabile eseguire il rerouting vocale per la modalità di sola ricezione dei messaggi. Accesso sottoscrittore consente agli utenti interni di accedere alla cassetta postale di Microsoft Outlook da un telefono. I numeri forniti da queste impostazioni consentono ai chiamanti di lasciare messaggi vocali per gli utenti VoIP aziendale (impostazione AutoAttendantNumber) e di recuperare i messaggi vocali anche se non è disponibile la connettività IP dalla distribuzione di Lync Server in un sito remoto con la Messaggistica unificata di Exchange nel data center (impostazione SubscriberAccessNumber).

L'utilizzo di questo cmdlet senza parametri restituirà tutte le configurazioni relative al rerouting della segreteria telefonica.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsVoicemailReroutingConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoicemailReroutingConfiguration"}

## Parametri


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il parametro Filter consente di recuperare le impostazioni di configurazione per un gruppo particolare di siti in base alla corrispondenza dei caratteri jolly.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'identificatore univoco della configurazione che si desidera recuperare. Per questo cmdlet l'identità sarà Global o Site:&lt;nome sito&gt;, in cui &lt;nome sito&gt; indica il nome del sito a cui sono applicate le impostazioni.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare la configurazione del rerouting della segreteria telefonica dalla copia locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Consente di recuperare uno o più oggetti di tipo Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsVoicemailReroutingConfiguration](new-csvoicemailreroutingconfiguration.md)  
[Remove-CsVoicemailReroutingConfiguration](remove-csvoicemailreroutingconfiguration.md)  
[Set-CsVoicemailReroutingConfiguration](set-csvoicemailreroutingconfiguration.md)

