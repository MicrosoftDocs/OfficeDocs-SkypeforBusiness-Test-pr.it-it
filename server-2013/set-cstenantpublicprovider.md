---
title: Set-CsTenantPublicProvider
TOCTitle: Set-CsTenantPublicProvider
ms:assetid: 8341d801-bfa1-4c5b-9b80-5d503deebaf7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994047(v=OCS.15)
ms:contentKeyID: 52062189
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTenantPublicProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Abilita e disabilita le comunicazioni con i provider di servizi di messaggistica istantanea e di presenza di terze parti Windows Live, AOL e Yahoo. Se le comunicazioni sono abilitate, gli utenti di Microsoft Lync Online potranno scambiare messaggi istantanei e informazioni sulla presenza con gli utenti con account presso il provider pubblico specificato.

Il cmdlet **Set-CsTenantPublicProvider** può essere usato solo con Skype for Business online.

## Sintassi

    Set-CsTenantPublicProvider -Tenant <String> [-Provider <String[]>] [-Verbose] [-WhatIf] [-Confirm]

## Esempi

## Esempio 1

Il comando illustrato nell'esempio 1 abilita la federazione con Windows Live per il tenant con ID bf19b7db-6960-41e5-a139-2aa373474354. Dato che Windows Live è l'unico provider specificato, entrambi i provider AOL e Yahoo verranno disabilitati dopo l'esecuzione del comando.

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive"

## Esempio 2

Nell'esempio 2 vengono abilitati due provider pubblici, ovvero Windows Live e AOL. Questo significa che per il tenant specificato verrà disabilitato solo il provider pubblico Yahoo.

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive","AOL"

## Esempio 3

L'esempio 3 illustra come disabilitare tutti i provider pubblici per un determinato tenant. L'operazione viene eseguita impostando la proprietà Provider su una stringa vuota ("").

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider ""

## Esempio 4

Il comando illustrato nell'esempio 4 disabilita tutti i provider pubblici per tutti i tenant di Lync Online. Per ottenere questo risultato, il comando usa prima di tutto il cmdlet **Get-CsTenant** per restituire una raccolta di tutti i tenant. La raccolta viene poi inviata tramite pipe al cmdlet **ForEach-Object** che chiama il cmdlet **Set-CsTenantPublicProvider** per ogni tenant della raccolta e disabilita tutti i provider pubblici. Quest'ultima operazione viene eseguita impostando la proprietà Provider su una stringa vuota ("").

    Get-CsTenant | ForEach-Object {Set-CsTenantPublicProvider -Tenant $_.TenantId -Provider ""}

## Descrizione dettagliata

I provider pubblici sono organizzazioni che forniscono servizi di comunicazione SIP al pubblico. Quando si configura una relazione di federazione con un provider pubblico, la federazione viene in realtà estesa a chiunque disponga di un account ospitato da tale provider. Se ad esempio si abilita la federazione con Windows Live, gli utenti potranno scambiare messaggi istantanei e informazioni sulla presenza con chiunque disponga di un account di messaggistica istantanea di Windows Live.

Lync Online offre agli amministratori la possibilità di configurare la federazione con uno o più dei provider di servizi di messaggistica istantanea o di presenza pubblici seguenti:

  -   
    Windows Live

  -   
    AOL

  -   
    Yahoo\!

È possibile usare il cmdlet **Set-CsTenantPublicProvider** per abilitare o disabilitare la federazione con qualsiasi provider pubblico tra questi. Quando si usa questo cmdlet, tenere presente che ogni volta che si esegue il cmdlet **Set-CsTenantPublicProvider** è necessario specificare tutti i provider da abilitare. Si supponga, ad esempio, che tutti e tre i provider siano disabilitati e di eseguire questo comando:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive"

Come prevedibile, verrà abilitato il provider Windows Live e i provider AOL e Yahoo rimarranno disabilitati.

Si supponga ora di eseguire poi questo comando:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "AOL"

Questo comando abilita AOL, ma disabilita anche Windows Live perché Windows Live non è specificato nel valore fornito al parametro Provider. Per abilitare AOL e mantenere abilitato anche Windows Live, è necessario specificare sia AOL che Windows Live quando si chiama Set-CsTenantPublicProvider:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "AOL","WindowsLive"

Per disabilitare la federazione per tutti e tre i provider, impostare la proprietà Provider su una stringa vuota ("").

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider ""

Si noti che la semplice abilitazione dello stato di un provider pubblico non significa che gli utenti siano in grado di scambiare messaggi istantanei e informazioni sulla presenza con gli utenti che hanno account con tale provider. Oltre ad abilitare la federazione con il provider in questione, gli amministratori devono anche impostare su True la proprietà AllowPublicUsers delle impostazioni di configurazione della federazione. Se la proprietà è impostata su False, le comunicazioni non saranno consentite con alcun provider pubblico, indipendentemente dalle impostazioni di configurazione del provider pubblico.

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
<td><p><em>Tenant</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di cui vengono modificate le impostazioni dei provider pubblici. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<pre><code>Get-CsTenant | Select-Object DisplayName, TenantID</code></pre>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Provider</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String[]</p></td>
<td><p>Indica il provider o i provider pubblici con i quali gli utenti saranno autorizzati a comunicare. I valori validi sono:</p>
<p>* AOL</p>
<p>* WindowsLive</p>
<p>* Yahoo</p>
<p>Si noti che per la configurazione dei provider pubblici, qualsiasi provider incluso nel valore del parametro Provider sarà abilitato per l'uso, mentre qualsiasi provider non incluso sarà disabilitato. La sintassi seguente, ad esempio, abilita solo Yahoo e disabilita al tempo stesso Windows Live e AOL:</p>
<p>-Provider &quot;AOL&quot;</p>
<p>Per abilitare più provider è possibile separare i nomi dei provider con virgole:</p>
<p>-Provider &quot;AOL&quot;,&quot;WindowsLive&quot;</p></td>
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

Il cmdlet **Set-CsTenantPublicProvider** accetta le istanze inviate tramite pipeline dell'oggetto Microsoft.Rtc.Management.Hosted.TenantPICStatus.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsTenantPublicProvider** modifica invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.Hosted.TenantPICStatus.

## Vedere anche

#### Ulteriori risorse

[Get-CsTenantPublicProvider](get-cstenantpublicprovider.md)

