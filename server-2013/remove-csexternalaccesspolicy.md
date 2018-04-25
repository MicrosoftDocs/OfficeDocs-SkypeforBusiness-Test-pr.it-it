---
title: Remove-CsExternalAccessPolicy
TOCTitle: Remove-CsExternalAccessPolicy
ms:assetid: eae27b8f-0c25-4723-95e9-435e36f06a79
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399057(v=OCS.15)
ms:contentKeyID: 49302380
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsExternalAccessPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di rimuovere un criterio di accesso esterno esistente. I criteri di accesso esterno determinano se gli utenti possono eseguire le operazioni seguenti: 1) comunicare con utenti che dispongono di account SIP (Session Initiation Protocol) con un'organizzazione federata, 2) comunicare con utenti che dispongono di account SIP con un provider di servizi di messaggistica istantanea pubblico come Windows Live e 3) accedere a Lync Server tramite Internet, senza dover effettuare l'accesso alla rete interna. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsExternalAccessPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1, il criterio di accesso esterno con il parametro Identity site:Redmond viene eliminato. Una volta rimosso tale criterio, per gli utenti del sito Redmond le autorizzazioni di accesso esterno saranno controllate dal criterio globale.

    Remove-CsExternalAccessPolicy -Identity site:Redmond

## ESEMPIO 2

Nell'esempio 2 vengono eliminati tutti i criteri di accesso esterno configurati nell'ambito del sito. Per eseguire questa attività, nel comando vengono innanzitutto utilizzati il cmdlet **Get-CsExternalAccessPolicy** e il parametro Filter per restituire una raccolta dei criteri configurati nell'ambito del sito. Il valore di filtro "site:\*" limita i dati restituiti ai criteri di accesso esterno il cui valore Identity inizia con il valore stringa "site:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsExternalAccessPolicy**, che elimina ogni criterio della raccolta.

    Get-CsExternalAccessPolicy -Filter site:* | Remove-CsExternalAccessPolicy 

## ESEMPIO 3

Nell'esempio 3 vengono eliminati tutti i criteri di accesso esterno che consentono l'accesso federato. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsExternalAccessPolicy** per restituire una raccolta di tutti i criteri di accesso esterno configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri la cui proprietà EnableFederationAccess è uguale a True. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsExternalAccessPolicy**, che elimina ogni criterio della raccolta.

    Get-CsExternalAccessPolicy | Where-Object {$_.EnableFederationAccess -eq $True} | Remove-CsExternalAccessPolicy 

## ESEMPIO 4

Nell'esempio 4 vengono eliminati tutti i criteri di accesso esterno che soddisfano almeno uno dei due criteri seguenti: accesso federato consentito, accesso cloud pubblico consentito o entrambi i tipi di accesso consentiti. Per eseguire questa attività, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsExternalAccessPolicy** per restituire una raccolta di tutti i criteri di accesso esterno configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri che soddisfano le seguenti condizioni: EnableFederationAccess uguale a True e/o EnablePublicCloudAccess uguale a True. I criteri che soddisfano una o entrambe queste condizioni vengono quindi inviati tramite pipe e rimossi dal cmdlet **Remove-CsExternalAccessPolicy**.

Per eliminare tutti i criteri in cui le proprietà EnableFederationAccess e EnablePublicCloudAccess sono entrambe impostate su True, utilizzare l'operatore –and quando viene chiamato il cmdlet **Where-Object**:

Where-Object {$\_.EnableFederationAccess -eq $True -and $\_.EnablePublicCloudAccess -eq $True}

    Get-CsExternalAccessPolicy | Where-Object {$_.EnableFederationAccess -eq $True -or $_.EnablePublicCloudAccess -eq $True} | Remove-CsExternalAccessPolicy 

## Descrizione dettagliata

Quando si installa Lync Server, agli utenti è consentito unicamente lo scambio reciproco di messaggi istantanei e di informazioni sulla presenza: per impostazione predefinita, comunicano solo con altri utenti che dispongono di account SIP in Servizi di dominio Active Directory. Agli utenti non è inoltre consentito accedere a Lync Server tramite Internet, ma è necessario effettuare l'accesso alla rete interna per poter quindi accedere a Lync Server.

1\. Tutto ciò potrebbe soddisfare le esigenze di comunicazione. Se le esigenze di comunicazione non vengono soddisfatte, è possibile utilizzare i criteri di accesso esterno per ampliare le possibilità di comunicazione e collaborazione degli utenti. Con i criteri di accesso esterno è possibile concedere (o revocare) agli utenti la possibilità di eseguire una o tutte le operazioni seguenti:

2\. Comunicare con persone che dispongono di account SIP con un'organizzazione federata. La sola abilitazione della federazione non offrirà agli utenti questa funzionalità. È invece necessario abilitare la federazione, quindi assegnare agli utenti il criterio di accesso esterno che concede il diritto di comunicare con utenti federati.

3\. Comunicare con persone che dispongono di account SIP con un servizio di messaggistica istantanea pubblico come Windows Live.

Accedere a Lync Server tramite Internet, senza dover prima effettuare l'accesso alla rete interna. Ciò consente agli utenti di utilizzare Lync e di accedere a Lync Server da un Internet café o da un'altra postazione remota.

Quando si installa Lync Server, viene creato automaticamente un criterio di accesso esterno globale. Oltre al criterio globale, è possibile utilizzare il cmdlet **New-CsExternalAccessPolicy** per creare criteri di accesso esterno configurati nell'ambito del sito o nell'ambito per utente.

Il cmdlet **Remove-CsExternalAccessPolicy** consente di eliminare i criteri creati mediante il cmdlet **New-CsExternalAccessPolicy**. In tal modo è possibile eliminare i criteri assegnati all'ambito del sito o all'ambito per utente. È possibile eseguire il cmdlet **Remove-CsExternalAccessPolicy** anche sul criterio di accesso esterno globale. In tal caso, tuttavia, i criteri globali non verranno eliminati; per impostazione predefinita, non è possibile eliminare i criteri globali. Le proprietà del criterio globale verranno semplicemente reimpostate sui valori predefiniti.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Remove-CsExternalAccessPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsExternalAccessPolicy"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per il criterio di accesso esterno da rimuovere. È possibile configurare i criteri di accesso con ambito globale, nell'ambito del sito o nell'ambito per utente. Per rimuovere il criterio globale, utilizzare la seguente sintassi: -Identity global. Non è possibile rimuovere effettivamente il criterio globale. Le proprietà del criterio globale verranno semplicemente reimpostate sui valori predefiniti. Per rimuovere un criterio del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Per rimuovere un criterio per utente, utilizzare una sintassi simile alla seguente: -Identity SalesAccessPolicy.</p>
<p>Non sono consentiti caratteri jolly per specificare un parametro Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ExternalAccess.ExternalAccessPolicy. Il cmdlet **Remove-CsExternalAccessPolicy** accetta l'input da pipeline dell'oggetto criterio di accesso esterno.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsExternalAccessPolicy** non restituisce alcun oggetto o valore. Il cmdlet piuttosto configura le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ExternalAccess.ExternalAccessPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsExternalAccessPolicy](get-csexternalaccesspolicy.md)  
[Grant-CsExternalAccessPolicy](grant-csexternalaccesspolicy.md)  
[New-CsExternalAccessPolicy](new-csexternalaccesspolicy.md)  
[Set-CsExternalAccessPolicy](set-csexternalaccesspolicy.md)

