---
title: New-CsFIPSConfiguration
TOCTitle: New-CsFIPSConfiguration
ms:assetid: 9ce030fb-fb6b-47a2-9fb9-69e8369b43be
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205114(v=OCS.15)
ms:contentKeyID: 49301461
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsFIPSConfiguration

 

_**Ultima modifica dell'argomento:** 2014-10-29_

Crea una nuova raccolta di impostazioni di configurazione FIPS (Federal Information Processing Standards). Gli standard FIPS sono un insieme di standard di sicurezza del Governo degli Stati Uniti da utilizzare nei computer gestiti da agenzie governative non militari e da appaltatori governativi. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsFIPSConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-RequireFIPSCompliantMedia <$true | $false>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

I comandi riportati nell'esempio 1 creano un nuovo insieme di impostazioni di configurazione FIPS solo in memoria e quindi utilizzano tali impostazioni per aggiornare la raccolta globale di impostazioni di configurazione FIPS. A tale scopo, nel primo comando dell'esempio vengono utilizzati il cmdlet **New-CsFIPSConfiguration** e il parametro InMemory per creare una nuova raccolta di impostazioni di configurazione FIPS con identità (Identity) "global". L'oggetto impostazioni risultante viene archiviato in una variabile denominata $x.

Nel secondo comando vengono quindi utilizzati il cmdlet **Set-CsFIPSConfiguration** e il parametro Instance per sostituire la raccolta globale esistente di impostazioni FIPS con la nuova raccolta archiviata in $x.

Anche se questo esempio funziona, è più semplice modificare le impostazioni di configurazione FIPS utilizzando il cmdlet **Set-CsFIPSConfiguration**.

    $x = New-CsFIPSConfiguration -Identity "global" -RequireFIPSCompliantMedia $False -InMemory
    
    Set-CsFIPSConfiguration -Instance $x

## Descrizione dettagliata

Gli standard FIPS (Federal Information Processing Standards) sono una serie di linee guida e di standard applicati a computer utilizzati per collaborare con il Governo degli Stati Uniti. Alcuni standard FIPS ad esempio definiscono l'utilizzo di elementi quali la crittografia e le firme digitali. Per ulteriori informazioni, vedere la pagina Web all'indirizzo <http://www.itl.nist.gov/fipspubs/by-num.htm>. In Lync Server 2013 è disponibile un'opzione che consente al software di utilizzare solo algoritmi che soddisfano gli standard FIPS. In caso di collaborazione con il Governo degli Stati Uniti o con altri enti che applicano gli standard FIPS, è possibile abilitare la conformità FIPS in Lync Server 2013.

Considerare tuttavia che per la versione locale di Lync Server è disponibile una singola raccolta globale di impostazioni di configurazione FIPS. È possibile pertanto abilitare o disabilitare la conformità FIPS solo per l'intera implementazione di Lync Server e non in modo selettivo ad esempio per un singolo sito o per un singolo pool di registrazione. Se si abilita la conformità FIPS, esiste il rischio che si verifichino problemi di comunicazione con organizzazioni che non aderiscono pienamente agli standard FIPS. Questo significa che il cmdlet **New-CsFIPSConfiguration** cmdlet viene utilizzato principalmente per gestire la conformità FIPS per Skype for Business online.

Per impostazione predefinita, la conformità FIPS è disabilitata in Lync Server 2013.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsFIPSConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet New-CsFIPSConfiguration non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Identificatore univoco della nuova raccolta di impostazioni FIPS. Poiché Lync Server 2013 supporta solo una raccolta globale di impostazioni FIPS, l'unico modo per poter utilizzare questo parametro è quello di creare una &quot;nuova&quot; raccolta globale esistente solo in memoria. A tale scopo, sarà inoltre necessario utilizzare il parametro InMemory.</p></td>
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
<td><p><em>RequireFIPSCompliantMedia</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se questo parametro è impostato su True, Lync Server 2013 consentirà solo sessioni multimediali con entità che utilizzano algoritmi conformi agli standard FIPS per l'autenticazione e l'autorizzazione.</p>
<p>Se si richiede la conformità agli standard FIPS, gli utenti non potranno più connettersi al sistema utilizzando un A/V Edge Server di Microsoft Lync Server 2010. Sarà invece necessario aggiornare tutti i server perimetrali a Lync 2013.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account del tenant di Skype for Business online per cui vengono create nuove impostazioni di configurazione FIPS, ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID tenant per ciascun tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Nessuno. Il cmdlet **New-CsFIPSConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **New-CsFIPSConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.FIPSConfiguration.FIPSConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsFIPSConfiguration](get-csfipsconfiguration.md)  
[Remove-CsFIPSConfiguration](remove-csfipsconfiguration.md)  
[Set-CsFIPSConfiguration](set-csfipsconfiguration.md)

