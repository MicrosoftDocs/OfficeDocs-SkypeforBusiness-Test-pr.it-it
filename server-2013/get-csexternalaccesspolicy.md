---
title: Get-CsExternalAccessPolicy
TOCTitle: Get-CsExternalAccessPolicy
ms:assetid: 301403c8-aeb2-4501-a2ae-96eaa6ad68a4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425805(v=OCS.15)
ms:contentKeyID: 49300081
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsExternalAccessPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce le informazioni sui criteri di accesso esterno configurati per l'utilizzo nell'organizzazione. I criteri di accesso esterno determinano se gli utenti possono eseguire le operazioni seguenti: 1) comunicare con utenti che dispongono di account SIP (Session Initiation Protocol) con un'organizzazione federata, 2) comunicare con utenti che dispongono di account SIP con un provider di servizi di messaggistica istantanea pubblico come Windows Live e 3) accedere a Lync Server tramite Internet, senza dover effettuare l'accesso alla rete interna. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsExternalAccessPolicy [-Identity <XdsIdentity>] [[-ApplicableTo] <Object>] <COMMON PARAMETERS>

    Get-CsExternalAccessPolicy [-Filter <String>] [[-ApplicableTo] <Object>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene restituita una raccolta di tutti i criteri di accesso esterno configurati per l'utilizzo nell'organizzazione. Se si chiama il cmdlet **Get-CsExternalAccessPolicy** senza parametri aggiuntivi, viene sempre restituita l'intera raccolta di criteri di accesso esterno.

    Get-CsExternalAccessPolicy

## ESEMPIO 2

Con l'esempio 2 viene utilizzato il parametro Identity per restituire il criterio di accesso esterno con Identity site:Redmond. Poiché le identità dei criteri di accesso devono essere univoche, questo comando non restituisce mai più di un elemento.

    Get-CsExternalAccessPolicy -Identity site:Redmond

## ESEMPIO 3

Con il comando mostrato nell'esempio 3 viene utilizzato il parametro Filter per restituire tutti i criteri di accesso esterno configurati nell'ambito per utente; il valore del parametro "tag:\*" limita i dati restituiti ai criteri la cui identità inizia con il valore stringa "tag:". Per definizione, tutti i criteri con una identità che inizia con "tag:" sono criteri configurati nell'ambito per utente.

    Get-CsExternalAccessPolicy -Filter tag:*

## ESEMPIO 4

Nell'esempio 4 vengono utilizzati i cmdlet **Get-CsExternalAccessPolicy** e **Where-Object** per restituire tutti i criteri di accesso esterno che concedono agli utenti l'accesso alla federazione. A tale scopo, viene innanzitutto utilizzato il cmdlet **Get-CsExternalAccessPolicy** per restituire una raccolta di tutti i criteri di accesso esterno attualmente in uso nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe a **Where-Object**, che seleziona unicamente i criteri in cui la proprietà EnableFederationAccess è uguale a True.

    Get-CsExternalAccessPolicy | Where-Object {$_.EnableFederationAccess -eq $True}

## ESEMPIO 5

Il comando riportato nell'esempio 5 restituisce i criteri di accesso esterno che soddisfano i due criteri seguenti: sono consentiti sia l'accesso alla federazione sia l'accesso al cloud pubblico. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsExternalAccessPolicy** per restituire una raccolta di tutti i criteri di accesso in uso nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri che soddisfano i due criteri seguenti: la proprietà EnableFederationAccess deve essere uguale a True e, allo stesso modo, la proprietà EnablePublicCloudAccess deve essere uguale a True. Verranno restituiti e visualizzati solo i criteri in cui entrambe le proprietà, EnableFederationAccess e EnablePublicCloudAccess, sono impostate su True.

Per restituire un elenco dei criteri in cui sia EnableFederationAccess sia EnablePublicCloudAccess sono True, utilizzare l'operatore -or:

Where-Object {$\_.EnableFederationAccess -eq $True -or $\_.EnablePublicCloudAccess -eq $True}

    Get-CsExternalAccessPolicy | Where-Object {$_.EnableFederationAccess -eq $True -and $_.EnablePublicCloudAccess -eq $True} 

## Descrizione dettagliata

Quando si installa Lync Server, agli utenti è consentito unicamente lo scambio reciproco di messaggi istantanei e di informazioni sulla presenza: per impostazione predefinita, comunicano solo con altri utenti che dispongono di account SIP in Servizi di dominio Active Directory. Agli utenti non è inoltre consentito accedere a Lync Server tramite Internet, ma è necessario effettuare l'accesso alla rete interna per poter quindi accedere a Lync Server.

Tutto ciò potrebbe soddisfare le esigenze di comunicazione. Se le esigenze di comunicazione non vengono soddisfatte, è possibile utilizzare i criteri di accesso esterno per ampliare le possibilità di comunicazione e collaborazione degli utenti. Con i criteri di accesso esterno è possibile concedere (o revocare) agli utenti la possibilità di eseguire una o tutte le operazioni seguenti:

1\. Comunicare con persone che dispongono di account SIP con un'organizzazione federata. La sola abilitazione della federazione non offrirà agli utenti questa funzionalità. È invece necessario abilitare la federazione, quindi assegnare agli utenti il criterio di accesso esterno che concede il diritto di comunicare con utenti federati.

2\. Comunicare con persone che dispongono di account SIP con un servizio di messaggistica istantanea pubblico come Windows Live.

3\. Accedere a Lync Server tramite Internet, senza dover prima effettuare l'accesso alla rete interna. Ciò consente agli utenti di utilizzare Lync e di accedere a Lync Server da un Internet café o da un'altra postazione remota.

Il cmdlet **Get-CsExternalAccessPolicy** consente di visualizzare le informazioni su tutti i criteri di accesso esterno configurati per l'utilizzo nell'organizzazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Get-CsExternalAccessPolicy** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsExternalAccessPolicy"}

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
<td><p>Consente di eseguire una ricerca con caratteri jolly dei criteri dei criteri di accesso esterno. Ad esempio, per trovare tutti i criteri configurati nell'ambito del sito, utilizzare il filtro: site:*. Per trovare i criteri per utente Seattle, Seville e Saskatoon (ciascuno dei quali inizia con la lettera &quot;S&quot;), utilizzare il filtro: &quot;S*&quot;. Si noti che il parametro Filter può essere applicato solo al criterio Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità univoca assegnata al criterio al momento della creazione. I criteri di accesso esterno possono essere assegnati con ambito globale, sito o per utente. Per fare riferimento all'istanza globale, utilizzare la sintassi seguente: -Identity global. Per ottenere un criterio nell'ambito del sito, utilizzare la seguente sintassi: -Identity site:Redmond. Per fare riferimento a un criterio nell'ambito per utente, utilizzare la sintassi: -Identity RedmondPolicy.</p>
<p>Si noti che non è possibile utilizzare i caratteri jolly, come l'asterisco (*), con il parametro Identity. Per eseguire una ricerca con caratteri jolly dei criteri, utilizzare il parametro Filter.</p>
<p>Se non viene specificato né il parametro Identity né il parametro Filter, il cmdlet <strong>Get-CsExternalAccessPolicy</strong> restituirà una raccolta di tutti i criteri di accesso esterno configurati per l'utilizzo nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati dei criteri di accesso esterno dalla replica locale del archivio di gestione centrale anziché dal archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsExternalAccessPolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ExternalAccess.ExternalAccessPolicy.

## Vedere anche

#### Ulteriori risorse

[Grant-CsExternalAccessPolicy](grant-csexternalaccesspolicy.md)  
[New-CsExternalAccessPolicy](new-csexternalaccesspolicy.md)  
[Remove-CsExternalAccessPolicy](remove-csexternalaccesspolicy.md)  
[Set-CsExternalAccessPolicy](set-csexternalaccesspolicy.md)

