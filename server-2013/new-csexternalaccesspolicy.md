---
title: New-CsExternalAccessPolicy
TOCTitle: New-CsExternalAccessPolicy
ms:assetid: 624a878e-6bbf-4e8b-9a5e-e7b5521fa4c1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398441(v=OCS.15)
ms:contentKeyID: 49300769
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsExternalAccessPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di creare un nuovo criterio di accesso esterno. I criteri di accesso esterno determinano se gli utenti possono eseguire le operazioni seguenti: 1) comunicare con utenti che dispongono di account SIP (Session Initiation Protocol) con un'organizzazione federata, 2) comunicare con utenti che dispongono di account SIP con un provider di servizi di messaggistica istantanea pubblico come MSN e 3) accedere a Lync Server tramite Internet, senza dover effettuare l'accesso alla rete interna. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsExternalAccessPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnableFederationAccess <$true | $false>] [-EnableOutsideAccess <$true | $false>] [-EnablePublicCloudAccess <$true | $false>] [-EnablePublicCloudAudioVideoAccess <$true | $false>] [-EnableXmppAccess <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene creato un nuovo criterio di accesso esterno con identità site:Redmond; in fase di creazione il criterio viene automaticamente assegnato al sito Redmond. Questo nuovo criterio imposta entrambe le proprietà EnableFederationAccess ed EnableOutsideAccess su True.

    New-CsExternalAccessPolicy -Identity site:Redmond -EnableFederationAccess $True -EnableOutsideAccess $True

## ESEMPIO 2

Con l'esempio 2 viene dimostrato l'uso del parametro InMemory, che consente di creare un'istanza solo in memoria di un criterio di accesso esterno. Dopo la creazione, è possibile modificare l'istanza solo in memoria e poi utilizzare il cmdlet **Set-CsExternalAccessPolicy** per trasformare il criterio virtuale in un criterio di accesso esterno reale.

Per eseguire queste operazioni, il primo comando nell'esempio utilizza il cmdlet **New-CsExternalAccessPolicy** con il parametro InMemory per creare un criterio virtuale con identità (Identity) RedmondAccessPolicy. Questo criterio virtuale viene archiviato in una variabile denominata $x. I tre comandi successivi vengono utilizzati per modificare tre proprietà del criterio virtuale: EnableFederationAccess, EnablePublicCloudAccess ed EnableOutsideAccess. L'ultimo comando utilizza infine il cmdlet **Set-CsExternalAccessPolicy** per creare un criterio di accesso esterno per utente effettivo con identità (Identity) RedmondAccessPolicy. Se non si chiama il cmdlet **Set-CsExternalAccessPolicy**, il criterio virtuale scomparirà nel momento in cui si termina la sessione di Windows PowerShell o si elimina la variabile $x. In questo caso, il criterio di accesso esterno con identità (Identity) RedmondAccessPolicy non verrà mai creato.

``` 
$x = New-CsExternalAccessPolicy -Identity RedmondAccessPolicy -InMemory
$x.EnableFederationAccess = $True
$x.EnablePublicCloudAccess = $True
$x.EnableOutsideAccess = $True
Set-CsExternalAccessPolicy -Instance $x  
```

## Descrizione dettagliata

Quando si installa Lync Server, agli utenti è consentito unicamente lo scambio reciproco di messaggi istantanei e di informazioni sulla presenza: per impostazione predefinita, comunicano solo con altri utenti che dispongono di account SIP in Servizi di dominio Active Directory. Agli utenti non è inoltre consentito accedere a Lync Server tramite Internet, ma è necessario effettuare l'accesso alla rete interna per poter quindi accedere a Lync Server.

Tutto ciò potrebbe soddisfare le esigenze di comunicazione. In caso contrario, è possibile utilizzare i criteri di accesso esterno per estendere la possibilità degli utenti di comunicare e collaborare. I criteri di accesso esterno possono concedere (o revocare) agli utenti la capacità di eseguire una o più delle seguenti operazioni:

1\. Comunicare con persone che dispongono di account SIP con un'organizzazione federata. La sola abilitazione della federazione non offrirà agli utenti questa funzionalità. È invece necessario abilitare la federazione, quindi assegnare agli utenti il criterio di accesso esterno che concede il diritto di comunicare con utenti federati.

2\. Comunicare con persone che dispongono di account SIP con un servizio di messaggistica istantanea pubblico come MSN.

3\. Accedere a Lync Server tramite Internet, senza dover prima effettuare l'accesso alla rete interna. Ciò consente agli utenti di usare Lync Server e di accedere a Lync Server da un Internet café o da un'altra postazione remota.

Quando si installa Lync Server, viene creato automaticamente un criterio di accesso esterno globale. Oltre al criterio globale, è possibile creare criteri di accesso esterno personalizzati nell'ambito del sito o per utente. Se si crea un criterio di accesso esterno nell'ambito del sito, il criterio viene automaticamente assegnato al sito in fase di creazione. Se si crea un criterio di accesso esterno nell'ambito per utente, il criterio viene creato ma non viene assegnato ad alcun utente. Per assegnare il criterio a un utente o a un gruppo di utenti, utilizzare il cmdlet **Grant-CsExternalAccessPolicy**.

I nuovi criteri di accesso esterno possono essere creati utilizzando il cmdlet **New-CsExternalAccessPolicy**. Questi criteri possono essere creati solamente nell'ambito del sito o per utente. Non è possibile creare un nuovo criterio nell'ambito globale. È possibile inoltre disporre di un solo criterio di accesso esterno per sito: se al sito Redmond è già stato assegnato un criterio di accesso esterno, non è possibile creare un secondo criterio per il sito.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsExternalAccessPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

    Get-CsAdminRole | Where-Object  {$_.Cmdlets -match "New-CsExternalAccessPolicy"}

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
<td><p>Identità univoca da assegnare al criterio. I nuovi criteri di accesso esterno possono essere creati nell'ambito del sito o per utente. Per creare un nuovo criterio di sito, utilizzare il prefisso &quot;site:&quot; e il nome del sito come identità. Ad esempio, utilizzare questa sintassi per creare un nuovo criterio per il sito Redmond: -Identity site:Redmond. Per creare un nuovo criterio per utente utilizzare un'identità simile alla seguente: -Identity SalesAccessPolicy.</p>
<p>Notare che non è possibile creare nuovi criteri globali. Se si desidera apportare modifiche ai criteri globali, utilizzare invece il cmdlet <strong>Set-CsExternalAccessPolicy</strong>. Analogamente, non è possibile creare nuovi criteri di sito o per utente se esistono già criteri con tale identità. Se è necessario apportare modifiche a criteri esistenti, utilizzare il cmdlet <strong>Set-CsExternalAccessPolicy</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire testo di spiegazione che accompagna i criteri. La descrizione può, ad esempio, includere informazioni sugli utenti a cui i criteri devono essere assegnati.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableFederationAccess</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se all'utente è consentito comunicare con persone che dispongono di account SIP con un'organizzazione federata. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableOutsideAccess</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se all'utente è consentito connettersi a Lync Server tramite Internet, senza dover effettuare l'accesso alla rete interna dell'organizzazione. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePublicCloudAccess</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se all'utente è consentito comunicare con persone che dispongono di account SIP con un provider di connettività Internet pubblica come MSN. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePublicCloudAudioVideoAccess</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se all'utente è consentito effettuare conversazioni audio/video con persone che dispongono di account SIP con un provider Internet pubblico come MSN. Se si imposta questo parametro su False, le opzioni audio e video in Lync Server vengono disabilitate ogni volta che un utente comunica con un contatto che utilizza la connettività Internet pubblica.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableXmppAccess</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se all'utente è consentito comunicare con utenti che dispongono di account SIP con un partner XMPP (Extensible Messaging and Presence Protocol) federato. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
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

Nessuno. Il cmdlet **New-CsExternalAccessPolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ExternalAccess.ExternalAccessPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsExternalAccessPolicy](get-csexternalaccesspolicy.md)  
[Grant-CsExternalAccessPolicy](grant-csexternalaccesspolicy.md)  
[Remove-CsExternalAccessPolicy](remove-csexternalaccesspolicy.md)  
[Set-CsExternalAccessPolicy](set-csexternalaccesspolicy.md)

