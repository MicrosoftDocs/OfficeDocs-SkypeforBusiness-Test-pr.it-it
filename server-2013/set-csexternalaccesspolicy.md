---
title: Set-CsExternalAccessPolicy
TOCTitle: Set-CsExternalAccessPolicy
ms:assetid: d3e45fbb-357f-4ff2-b52d-58b94e8f2241
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398916(v=OCS.15)
ms:contentKeyID: 49302072
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsExternalAccessPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di modificare le proprietà di un criterio di accesso esterno esistente. I criteri di accesso esterno determinano se gli utenti possono eseguire le operazioni seguenti: 1) comunicare con utenti che dispongono di account SIP (Session Initiation Protocol) con un'organizzazione federata, 2) comunicare con utenti che dispongono di account SIP con un provider di servizi di messaggistica istantanea pubblico come MSN e 3) accedere a Lync Server tramite Internet, senza dover effettuare l'accesso alla rete interna. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsExternalAccessPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsExternalAccessPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnableFederationAccess <$true | $false>] [-EnableOutsideAccess <$true | $false>] [-EnablePublicCloudAccess <$true | $false>] [-EnablePublicCloudAudioVideoAccess <$true | $false>] [-EnableXmppAccess <$true | $false>] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 modifica il criterio di accesso esterno per utente con valore Identity RedmondExternalAccessPolicy. Nell'esempio il comando cambia il valore della proprietà EnableFederationAccess impostandolo su True.

    Set-CsExternalAccessPolicy -Identity RedmondExternalAccessPolicy -EnableFederationAccess $True

## ESEMPIO 2

Nell'esempio 2 l'accesso della federazione viene abilitato per tutti i criteri di accesso esterno configurati per l'utilizzo nell'organizzazione. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsExternalAccessPolicy** senza parametri per restituire una raccolta di tutti i criteri di accesso esterno attualmente configurati per l'utilizzo. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsExternalAccessPolicy**, che cambia il valore della proprietà EnableFederationAccess per ogni criterio nella raccolta.

    Get-CsExternalAccessPolicy | Set-CsExternalAccessPolicy -EnableFederationAccess $True

## ESEMPIO 3

Nell'esempio 3 l'accesso della federazione viene consentito per tutti i criteri di accesso esterno configurati in ambito per utente. Per eseguire questa attività, nel comando vengono innanzitutto utilizzati il cmdlet **Get-CsExternalAcessPolicy** e il parametro Filter per restituire una raccolta di tutti i criteri configurati nell'ambito per utente. Il valore di filtro "tag:\*" limita i dati restituiti ai criteri in cui il parametro Identity inizia con il valore stringa "tag:", ovvero tutti i criteri con il parametro Identity che inizia con "tag:" sono stati configurati nell'ambito per utente. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsExternalAccessPolicy**, che modifica la proprietà EnableFederationAccess per ogni criterio nella raccolta.

    Get-CsExternalAccessPolicy -Filter tag:* | Set-CsExternalAccessPolicy -EnableFederationAccess $True

## ESEMPIO 4

Nell'esempio 4 l'accesso della federazione viene consentito per tutti i criteri di accesso esterno che consentono l'accesso cloud pubblico. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsExternalAccessPolicy** per restituire una raccolta di tutti i criteri di accesso esterno attualmente configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri con proprietà EnablePublicCloudAccess uguale a True. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsExternalAccessPolicy**, che imposta la proprietà EnableFederationAccess di ogni criterio su True. Ne risulta che tutti i criteri di accesso esterno che consentono l'accesso cloud pubblico consentiranno anche l'accesso della federazione.

    Get-CsExternalAccessPolicy | Where-Object {$_.EnablePublicCloudAccess -eq $True} | Set-CsExternalAccessPolicy -EnableFederationAccess $True

## Descrizione dettagliata

Quando si installa Lync Server, agli utenti è consentito unicamente lo scambio reciproco di messaggi istantanei e di informazioni sulla presenza: per impostazione predefinita, comunicano solo con gli utenti che dispongono di account SIP in Servizi di dominio Active Directory. Agli utenti non è inoltre consentito accedere a Lync Server tramite Internet, ma è necessario effettuare l'accesso alla rete interna per poter quindi accedere a Lync Server.

Tutto ciò potrebbe soddisfare le esigenze di comunicazione. Se le esigenze di comunicazione non vengono soddisfatte, è possibile utilizzare i criteri di accesso esterno per ampliare le possibilità di comunicazione e collaborazione degli utenti. Con i criteri di accesso esterno è possibile concedere (o revocare) agli utenti la possibilità di eseguire una o tutte le operazioni seguenti:

1\. Comunicare con persone che dispongono di account SIP con un'organizzazione federata. La sola abilitazione della federazione non offrirà agli utenti questa funzionalità. È invece necessario abilitare la federazione, quindi assegnare agli utenti il criterio di accesso esterno che concede il diritto di comunicare con utenti federati.

2\. Comunicare con persone che dispongono di account SIP con un servizio di messaggistica istantanea pubblico come MSN.

3\. Accedere a Lync Server tramite Internet, senza dover prima effettuare l'accesso alla rete interna. Ciò consente agli utenti di utilizzare Lync e di accedere a Lync Server da un Internet café o da un'altra postazione remota.

Dopo aver creato un criterio di accesso esterno, è possibile utilizzare il cmdlet **Set-CsExternalAccessPolicy** per modificare i valori delle proprietà del criterio. Per impostazione predefinita, ad esempio, il criterio globale non consente agli utenti di comunicare con persone che dispongono di account con un'organizzazione federata. Se si desidera concedere questa capacità a tutti i propri utenti, è possibile chiamare il cmdlet **Set-CsExternalAccessPolicy** e impostare il valore della proprietà EnableFederationAccess del criterio globale su True.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsExternalAccessPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsExternalAccessPolicy"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire un testo aggiuntivo da associare al criterio. Ad esempio, il parametro Description potrebbe includere informazioni sugli utenti a cui assegnare il criterio.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableFederationAccess</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se all'utente è consentito comunicare con persone che dispongono di account SIP con un'organizzazione federata. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableOutsideAccess</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se all'utente è consentito connettersi a Lync Server tramite Internet, senza dover effettuare l'accesso alla rete interna dell'organizzazione. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePublicCloudAccess</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se all'utente è consentito comunicare con persone che dispongono di account SIP con un provider di connettività Internet pubblica come MSN. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePublicCloudAudioVideoAccess</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se all'utente è consentito condurre conversazioni audio/video con persone che dispongono di account SIP con un provider Internet pubblico come MSN. Quando è impostato su False, le opzioni audio e video in Lync vengono disabilitate ogni volta che un utente comunica con un contatto che utilizza la connettività Internet pubblica. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableXmppAccess</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se all'utente è consentito comunicare con utenti che dispongono di account SIP con un partner XMPP (Extensible Messaging and Presence Protocol) federato. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per il criterio di accesso esterno da modificare. È possibile configurare i criteri di accesso con ambito globale, nell'ambito del sito o nell'ambito per utente. Per modificare il criterio globale, utilizzare la seguente sintassi: -Identity global. Per modificare un criterio di sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Per modificare un criterio per utente, utilizzare una sintassi simile alla seguente: -Identity SalesAccessPolicy. Se questo parametro non viene specificato, verrà modificato il criterio globale.</p>
<p>Non sono consentiti caratteri jolly per specificare un parametro Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>ExternalAccessPolicyObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ExternalAccess.ExternalAccessPolicy. Il cmdlet **Set-CsExternalAccessPolicy** accetta l'input da pipeline dell'oggetto criterio di accesso esterno.

## Tipi restituiti

Il cmdlet **Set-CsExternalAccessPolicy** non restituisce un valore o un oggetto. Il cmdlet configura piuttosto le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ExternalAccess.ExternalAccessPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsExternalAccessPolicy](get-csexternalaccesspolicy.md)  
[Grant-CsExternalAccessPolicy](grant-csexternalaccesspolicy.md)  
[New-CsExternalAccessPolicy](new-csexternalaccesspolicy.md)  
[Remove-CsExternalAccessPolicy](remove-csexternalaccesspolicy.md)

