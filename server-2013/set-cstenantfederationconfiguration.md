---
title: Set-CsTenantFederationConfiguration
TOCTitle: Set-CsTenantFederationConfiguration
ms:assetid: e13c2f55-7a68-4174-a0da-5eec8c65f64c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994080(v=OCS.15)
ms:contentKeyID: 52062458
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTenantFederationConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di gestire le impostazioni della configurazione della federazione per i tenant di Microsoft Lync Online. Queste impostazioni vengono usate per determinare con quali domini possono eventualmente comunicare gli utenti.

Il cmdlet **Set-CsTenantFederationConfiguration** può essere usato solo con Skype for Business online.

## Sintassi

    Set-CsTenantFederationConfiguration [[-Identity] <XdsIdentity>] [-Tenant <Nullable`1>] [-AllowedDomains <IAllowedDomainsChoice>] [-BlockedDomains <PSListModifier>] [-AllowFederatedUsers] [-AllowPublicUsers] [-SharedSipAddressSpace] [-Force] [-Verbose] [-WhatIf] [-Confirm]Set-CsTenantFederationConfiguration [-Tenant <Nullable`1>] [-AllowedDomains <IAllowedDomainsChoice>] [-BlockedDomains <PSListModifier>] [-AllowFederatedUsers] [-AllowPublicUsers] [-SharedSipAddressSpace] [-Instance <PSObject>] [-Force] [-Verbose] [-WhatIf] [-Confirm]

## Esempi

## Esempio 1

Il comando illustrato nell'esempio 1 disabilita la comunicazione con i provider pubblici per il tenant con ID "bf19b7db-6960-41e5-a139-2aa373474354".

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowPublicUsers $False

Si noti che il parametro Tenant è facoltativo. Se non lo si specifica, Windows PowerShell inserirà automaticamente l'ID del tenant corretto in base alle informazioni di connessione.

## Esempio 2

L'esempio 2 illustra come è possibile disabilitare la comunicazione con il provider pubblico per tutti i tenant dell'organizzazione. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsTenant** per fare in modo che venga restituita una raccolta di tutti i tenant disponibili. Tale raccolta viene quindi inoltrata tramite pipe al cmdlet **Select-Object** che seleziona solo la proprietà TenantId per ogni elemento della raccolta. La raccolta di ID dei tenant viene quindi inoltrata tramite pipe al cmdlet **ForEach-Object**. Il cmdlet F**orEach-Object** prende quindi ogni ID di tenant ed esegue il cmdlet **Set-CsTenantFederationConfiguration** in base a tale ID, impostando la proprietà AllowPublicUsers per ogni tenant su False ($False).

    Get-CsTenant | Select-Object TenantId | ForEach-Object {Set-CsTenantFederationConfiguration -Tenant $_.TenantId -AllowPublicUsers $False}

## Esempio 3

Nell'esempio 3 il dominio fabrikam.com viene assegnato come unico dominio nell'elenco di domini bloccati per il tenant con ID "bf19b7db-6960-41e5-a139-2aa373474354". A tale scopo, nel primo comando dell'esempio viene usato il cmdlet **New-CsEdgeDomainPattern** per creare un nuovo oggetto dominio per fabrikam.com. Tale oggetto dominio viene archiviato in una variabile denominata $x.

Nel secondo comando dell'esempio viene quindi usato il cmdlet **Set-CsTenantFederationConfiguration** per aggiornare l'elenco di domini bloccati. Il metodo Replace garantisce che l'elenco di domini bloccati esistente venga sostituito con il nuovo elenco che contiene solo il dominio fabrikam.com.

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant bf19b7db-6960-41e5-a139-2aa373474354 -BlockedDomains @{Replace=$x}

## Esempio 4

Mediante i comandi illustrati nell'esempio 4 il dominio fabrikam.com viene rimosso dall'elenco di domini bloccati dal tenant con ID "bf19b7db-6960-41e5-a139-2aa373474354". A tale scopo, nel primo comando dell'esempio viene usato il cmdlet **New-CsEdgeDomainPattern** per creare un oggetto dominio per fabrikam.com. L'oggetto dominio risultante viene quindi archiviato in una variabile denominata $x.

Nel secondo comando dell'esempio vengono quindi usati il cmdlet **Set-CsTenantFederationConfiguration** e il metodo Remove per rimuovere fabrikam.com dall'elenco di domini bloccati per il tenant specificato.

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant bf19b7db-6960-41e5-a139-2aa373474354 -BlockedDomains @{Remove=$x}

## Esempio 5

Mediante i comandi illustrati nell'esempio 5 il dominio fabrikam.com viene aggiunto all'elenco di domini bloccati dal tenant con ID "bf19b7db-6960-41e5-a139-2aa373474354". Per aggiungere un nuovo dominio bloccato, nel primo comando dell'esempio viene usato il cmdlet **New-CsEdgeDomainPattern** per creare un oggetto dominio per fabrikam.com. L'oggetto dominio viene quindi archiviato in una variabile denominata $x.

Dopo la creazione dell'oggetto dominio, nel secondo comando vengono quindi usati il cmdlet **Set-CsTenantFederationConfiguration** e il metodo Add per aggiungere fabrikam.com a tutti i domini già presenti nell'elenco di domini bloccati.

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant bf19b7db-6960-41e5-a139-2aa373474354 -BlockedDomains @{Add=$x}

## Esempio 6

Nell'esempio 6 viene illustrato come rimuovere tutti i domini assegnati all'elenco di domini bloccati per un determinato tenant. A tale scopo, è sufficiente includere il parametro BlockedDomains e impostarne il valore su Null ($Null). Al completamento del comando, l'elenco di domini bloccati per il tenant con ID "bf19b7db-6960-41e5-a139-2aa373474354" verrà cancellato.

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains $Null

## Descrizione dettagliata

Il servizio di federazione consente agli utenti di scambiarsi informazioni di messaggistica istantanea e sulla presenza con utenti di altri domini. Con Lync Online gli amministratori possono usare le impostazioni di configurazione della federazione per gestire:

  -   
    La possibilità per gli utenti di comunicare con utenti di altri domini ed eventualmente con quali domini possono comunicare.

  -   
    La possibilità per gli utenti di comunicare con altri utenti che dispongono di account presso un servizio di messaggistica istantanea o presso un provider della presenza pubblico come Windows Live, AOL e Yahoo.

Gli amministratori possono usare il cmdlet **Set-CsTenantFederationConfiguration** per abilitare e disabilitare la federazione con altri domini e la federazione con provider pubblici. Questo cmdlet può inoltre essere usato per indicare in modo esplicito i domini con cui gli utenti possono comunicare e/o i domini con cui non possono comunicare. Gli amministratori devono comunque usare il cmdlet **Set-CsTenantPublicProvider** per indicare i servizi di messaggistica istantanea e i provider della presenza pubblici con cui gli utenti possono e non possono comunicare.

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
<td><p><em>AllowedDomains</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Edge.IAllowedDomainsChoice</p></td>
<td><p>Oggetti dominio (creati mediante il cmdlet <strong>New-CsEdgeAllowList</strong> o <strong>New-CsEdgeAllowAllKnownDomains</strong>) che rappresentano i domini con cui gli utenti possono comunicare. Se viene usato il cmdlet <strong>New-CsEdgeAllowAllKnownDomains</strong>, gli utenti possono comunicare con qualsiasi dominio non incluso nell'elenco di domini bloccati. Se viene usato il cmdlet <strong>New-CsEdgeAllowList</strong>, gli utenti possono comunicare solo con i domini che sono stati aggiunti all'elenco di domini consentiti.</p>
<p>Si noti che i valori stringa non possono essere passati direttamente al parametro AllowedDomains. È infatti necessario creare un riferimento oggetto mediante il cmdlet <strong>New-CsEdgeAllowList</strong> o <strong>New-CsEdgeAllowAllKnownDomains</strong> e quindi usare la variabile del riferimento come valore del parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowFederatedUsers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato su True (valore predefinito) agli utenti è potenzialmente consentito comunicare con utenti di altri domini. Se è impostato su False, gli utenti non possono comunicare con utenti di altri domini indipendentemente dai valori assegnati alle proprietà AllowedDomains e BlockedDomains.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowPublicUsers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato su True (valore predefinito) agli utenti è potenzialmente consentito comunicare con altri utenti che dispongono di account presso un servizio di messaggistica istantanea o presso un provider della presenza pubblico come Windows Live, Yahoo e AOL. La raccolta di provider pubblici con cui gli utenti possono effettivamente comunicare viene gestita mediante il cmdlet Set-CsTenantPublicProvider.</p></td>
</tr>
<tr class="even">
<td><p><em>BlockedDomains</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se la proprietà AllowedDomains è impostata su AllowAllKnownDomains, gli utenti possono comunicare con gli utenti di tutti gli altri domini ad eccezione di quelli presenti nell'elenco di domini bloccati. Se la proprietà AllowedDomains non è impostata su AllowAllKnownDomains, l'elenco dei domini bloccati viene ignorato e gli utenti possono comunicare solo con i domini che sono stati esplicitamente aggiunti all'elenco dei domini consentiti.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Specifica la raccolta delle impostazioni di configurazione della federazione del tenant da modificare. Poiché ogni tenant è limitato a un'unica raccolta globale di impostazioni della federazione, non è necessario includere questo parametro quando si chiama il cmdlet <strong>Set-CsTenantFederationConfiguration</strong>. Se si sceglie di usare il parametro Identity, è inoltre necessario includere il parametro Tenant. Ad esempio:</p>
<p>Set-CsTenantFederationConfiguration -Tenant &quot;bf19b7db-6960-41e5-a139-2aa373474354&quot; –Identity &quot;global&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>SharedSipAddressSpace</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato su True, indica che gli utenti ospitati in Lync Online usano lo stesso dominio SIP degli utenti ospitati nella versione locale di Lync Server. Il valore predefinito è False, che significa che i due set di utenti dati usano domini SIP diversi.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant per cui modificare le impostazioni di federazione. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Eseguendo questo comando è possibile fare in modo che venga restituito l'ID di ogni tenant:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Se si usa una sessione remota di Windows PowerShell e si è connessi solo a Skype for Business online, non è necessario includere il parametro Tenant. L'ID del tenant verrà infatti compilato automaticamente in base alle informazioni di connessione. Il parametro Tenant è destinato principalmente all'uso in distribuzioni ibride.</p></td>
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

Il cmdlet **Set-CsTenantFederationConfiguration** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.TenantFederationSettings inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsTenantFederationConfiguration** modifica invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.TenantFederationSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md)

