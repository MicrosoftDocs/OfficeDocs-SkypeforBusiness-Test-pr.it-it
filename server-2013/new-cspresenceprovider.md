---
title: New-CsPresenceProvider
TOCTitle: New-CsPresenceProvider
ms:assetid: 55110f49-f8d5-4287-89d3-ae069d8090d3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204895(v=OCS.15)
ms:contentKeyID: 49300556
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPresenceProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Autorizza un nuovo provider del servizio di presenza per l'utilizzo nell'organizzazione. I provider di questo tipo rappresentano la proprietà PresenceProviders di una raccolta di impostazioni di configurazione di Servizi utente. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsPresenceProvider -Fqdn <String> -Parent <String> <COMMON PARAMETERS>

    New-CsPresenceProvider -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 crea un nuovo provider del servizio di presenza, con nome di dominio completo "fabrikam.com", che verrà aggiunto alla raccolta globale di impostazioni di configurazione di Servizi utente.

    New-CsPresenceProvider -Parent "global" -Fqdn "fabrikam.com"

## Esempio 2

Nell'esempio 2 viene aggiunto un provider del servizio di presenza con nome di dominio completo "fabrikam.com" a tutte le raccolte di configurazione di Servizi utente dell'organizzazione. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsUserServicesConfiguration** per restituire una raccolta di tutte le impostazioni di Servizi utente. Le impostazioni vengono quindi inviate tramite pipe al cmdlet ForEach-Object, che seleziona ogni elemento della raccolta e crea un nuovo provider del servizio di presenza per la raccolta utilizzando "fabrikam.com" come nome di dominio completo e l'identità della raccolta di Servizi utente come elemento padre del provider.

    Get-CsUserServicesConfiguration | ForEach-Object {New-CsPresenceProvider -Parent $_.Identity -Fqdn "fabrikam.com"}

## Descrizione dettagliata

I cmdlet **CsPresenceProvider** vengono utilizzati per gestire la proprietà PresenceProviders contenuta nelle impostazioni di configurazione di Servizi utente. Queste impostazioni vengono utilizzate ad esempio per gestire le informazioni sulla presenza, inclusa una raccolta di provider del servizio di presenza autorizzati. La raccolta viene archiviata nella proprietà PresenceProviders. È possibile utilizzare il cmdlet **New-CsPresenceProvider** per aggiungere un provider del servizio di presenza autorizzato a una raccolta di impostazioni di configurazione di Servizi utente.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPresenceProvider"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **New-CsPresenceProvider** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Fqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del provider del servizio di presenza, ad esempio:</p>
<p>-Fqdn &quot;fabrikam.com&quot;</p>
<p>Se si utilizza il parametro Fqdn, è necessario utilizzare anche il parametro Parent. Non è possibile tuttavia utilizzare il parametro Fqdn nello stesso comando del parametro Identity.</p>
<p>Si noti che i nomi di dominio completo devono essere univoci in un determinato ambito.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del nuovo provider del servizio di presenza. L'identità di un provider del servizio di presenza è costituita da due parti: l'ambito (parametro Parent) in cui è stato applicata la regola (ad esempio service:UserServer:atl-cs-001.litwareinc.com) e il nome di dominio completo del provider. Per creare un nuovo provider nell'ambito globale, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;global/fabrikam.com&quot;</p>
<p>Per creare un provider nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond/fabrikam.com&quot;</p>
<p>Per creare un provider nell'ambito del servizio (solo per il servizio UserServer), utilizzare una sintassi simile alla seguente:</p>
<p>-Parent &quot;UserServer:atl-cs-001.litwareinc.com&quot;</p>
<p>Non è possibile utilizzare il parametro Identity nello stesso comando del parametro Fqdn o Parent.</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Ambito in cui verrà creato il nuovo provider del servizio di presenza. Per creare un nuovo provider del servizio di presenza nell'ambito globale, utilizzare una sintassi simile alla seguente:</p>
<p>-Parent &quot;global&quot;</p>
<p>Per creare un nuovo provider nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Parent &quot;site:Redmond&quot;</p>
<p>Per creare un provider nell'ambito del servizio (solo per il servizio UserServer), utilizzare una sintassi simile alla seguente:</p>
<p>-Parent &quot;UserServer:atl-cs-001.litwareinc.com&quot;</p>
<p>Se si utilizza il parametro Parent, è necessario includere anche il parametro Fqdn. Non è possibile tuttavia utilizzare il parametro Parent insieme al parametro Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
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
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsPresenceProvider** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsPresenceProvider** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PresenceProvider\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsPresenceProvider](get-cspresenceprovider.md)  
[Get-CsUserServicesConfiguration](get-csuserservicesconfiguration.md)  
[Remove-CsPresenceProvider](remove-cspresenceprovider.md)  
[Set-CsPresenceProvider](set-cspresenceprovider.md)

