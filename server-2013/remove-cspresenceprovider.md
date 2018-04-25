---
title: Remove-CsPresenceProvider
TOCTitle: Remove-CsPresenceProvider
ms:assetid: 7e8b540e-484f-4003-8665-18e2b3974f33
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205036(v=OCS.15)
ms:contentKeyID: 49301108
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPresenceProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un provider del servizio di presenza precedentemente configurato per l'utilizzo nell'organizzazione. I provider di questo tipo rappresentano la proprietà PresenceProviders di una raccolta di impostazioni di configurazione di Servizi utente. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsPresenceProvider -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 rimuove il provider del servizio di presenza con l'identità "global/fabrikam.com".

    Remove-CsPresenceProvider -Identity "global/fabrikam.com"

## Esempio 2

Nell'esempio 2 vengono rimossi tutti i provider del servizio di presenza configurati per l'utilizzo nell'organizzazione. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsPresenceProvider** senza alcun parametro per restituire una raccolta di tutti i provider del servizio di presenza configurati. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsPresenceProvider**, che elimina ogni elemento (provider) della raccolta.

    Get-CsPresenceProvider | Remove-CsPresenceProvider

## Esempio 3

Nell'esempio 3 viene illustrato come eliminare tutti i provider del servizio di presenza con un nome di dominio completo (FQDN) che include il valore stringa "fabrikam.com". A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsPresenceProvider** per restituire una raccolta di tutti i provider del servizio di presenza disponibili. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i provider in cui la proprietà Fqdn include (-match) il valore stringa "fabrikam.com". Questa raccolta filtrata viene a sua volta inviata tramite pipe al cmdlet **Remove-CsPresenceProvider**, che elimina ogni provider della raccolta filtrata.

    Get-CsPresenceProvider | Where-Object {$_.Fqdn -match "fabrikam.com"} | Remove-CsPresenceProvider

## Descrizione dettagliata

I cmdlet **CsPresenceProvider** vengono utilizzati per gestire la proprietà PresenceProviders contenuta nelle impostazioni di configurazione di Servizi utente. Queste impostazioni vengono utilizzate ad esempio per gestire le informazioni sulla presenza, inclusa una raccolta di provider del servizio di presenza autorizzati. La raccolta viene archiviata nella proprietà PresenceProviders.

Il cmdlet **Remove-CsPresenceProvider** consente di rimuovere un provider del servizio di presenza dalla proprietà PresenceProviders di una o più raccolte di impostazioni di configurazione di Servizi utente.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPresenceProvider"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Remove-CsPresenceProvider** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Identificatore univoco del provider del servizio di presenza da rimuovere. Per rimuovere un singolo provider, utilizzare l'identità effettiva del provider, che include sia l'ambito sia il nome di dominio completo del provider:</p>
<p>-Identity &quot;global/fabrikam.com&quot;</p>
<p>Per rimuovere tutti i provider del servizio di presenza configurati in un determinato ambito, utilizzare semplicemente l'ambito come identità. La sintassi seguente consente di rimuovere tutti i provider configurati nell'ambito globale:</p>
<p>-Identity &quot;global&quot;</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Remove-CsPresenceProvider** accetta istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PresenceProvider\#Decorated inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsPresenceProvider** invece elimina istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PresenceProvider\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsPresenceProvider](get-cspresenceprovider.md)  
[Get-CsUserServicesConfiguration](get-csuserservicesconfiguration.md)  
[New-CsPresenceProvider](new-cspresenceprovider.md)  
[Set-CsPresenceProvider](set-cspresenceprovider.md)

